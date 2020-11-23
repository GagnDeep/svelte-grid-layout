<script>
  import { slide } from "svelte/transition";
  export let navbar;
  export let rightSidebar;
  export let leftSidebar;
  export let notification;

  let hovering;

  function handleLeftSidebarTrigger(event) {
    leftSidebar = true;
  }

  function handleRightSidebarTrigger(event) {
    rightSidebar = true;
  }

  function handleContentMouseover(event) {
    rightSidebar = false;
    leftSidebar = false;
  }

  function fadea(node, { delay = 0, duration = 200 }) {
    const o = 200;
    return {
      delay,
      duration,
      css: t => `width: ${t * o}px`
    };
  }
</script>

<style>
	@keyframes sidebar-keyframe {
	  from {
	    min-width: 0px;
	  }
	  to {
	    min-width: 200px;
	  }
	}

	.wrapper {
	  display: flex;
	}

	.left-sidebar {
	  width: 200px;
	}

	.right-sidebar {
	  width: 200px;
	}

	.content-container {
	  min-width: 400px;
	  flex-grow: grow;
	}
</style>

<div class="h-screen w-screen wrapper relative">

	<div on:mouseover={handleLeftSidebarTrigger} class="left-trigger absolute w-2 z-20 top-0 left-0 bottom-0" />
	<div on:mouseover={handleRightSidebarTrigger} class="right-trigger absolute w-2 z-20 top-0 right-0 bottom-0" />


  {#if leftSidebar}
    <div in:fadea={{direction: 'left'}} out:slide on:mouseover={handleLeftSidebarTrigger} class="left-sidebar bg-gray-200 z-30">
      <slot name="left"/>
    </div>
  {/if}

	<div on:mouseover={handleContentMouseover} class="content-container bg-gray-300 z-10 flex-grow">
		
		<slot name="center">
      <div class="navbar">
        
      </div>
      <div class="content"></div>
      <div class="notification"></div>
		</slot>
	</div>

  {#if rightSidebar}
    <div on:mouseover={handleRightSidebarTrigger} class="right-sidebar bg-gray-200 z-30" class:left-sidebar-active={rightSidebar}>
      <slot name="right"/>
    </div>
  {/if}
</div>