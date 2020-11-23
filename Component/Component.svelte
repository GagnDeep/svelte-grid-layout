<script>
	export let navbar;
	export let rightSidebar;
	export let leftSidebar;
	export let notification;

	let hovering;
</script>

<style>
	@keyframes abc {
	  from {
	    transform: translateX(-100%);
	  }
	  to {
	    transform: translateX(0);
	  }
	}

	.wrapper {
	  display: flex;
	}
	.inner-transition-left {
	  width: 200px;
	  transform: translateX(-100%);
	  transition: transform 0.2s ease-in-out;
	}

	.right-sidebar {
	  width: 0px;
	}
	.right-trigger:hover ~ .right-sidebar,
	.right-sidebar:hover {
	  width: 200px;
	  /* animation: sidebar-keyframe 0.2s ease-in-out forwards; */
	}

	.right-trigger:hover ~ .right-sidebar .inner-transition-left,
	.right-sidebar:hover .inner-transition-left {
	  /* transform: translateX(0); */
	  animation: abc 0.2s ease-in-out forwards;
	}

	.left-sidebar {
	  width: 0px;
	}
	.left-trigger:hover ~ .left-sidebar,
	.left-sidebar:hover {
	  width: 200px;
	}

	.left-sidebar-active {
	  animation: sidebar-keyframe 0.2s ease-in-out forwards;
	}

	.left-sidebar-active {
	  animation: sidebar-keyframe 0.2s ease-in-out forwards;
	}

	.content-container {
	  min-width: 400px;
	  flex-grow: grow;
	}
</style>

<div class="h-screen w-screen wrapper relative">

	<div class="right-trigger absolute w-2 z-20 top-0 left-0 bottom-0" />
	<div class="left-trigger absolute w-2 z-20 top-0 right-0 bottom-0" />


	<div class="right-sidebar bg-gray-200 z-30 overflow-visible">
		<div on:animationend={() => console.log('end')} class="inner-transition-left w-64 bg-gray-600 h-full">
			<slot name="left"/>
		</div>
	</div>

	<div class="content-container bg-gray-300 z-10 flex-grow">
		
		<slot name="center"/>
		<!-- <div class="navbar">
			
		</div>
		<div class="content"></div>
		<div class="notification"></div> -->
	</div>

	<div class="left-sidebar bg-gray-200 z-30" class:left-sidebar-active={rightSidebar}>
		<slot name="right"/>
	</div>

</div>