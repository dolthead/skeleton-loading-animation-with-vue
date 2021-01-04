<template functional>
	<span
		:style="{ height: props.height, width: $options.computedWidth(props) }"
		class="skeleton-box"
	/>
</template>

<script>
	export default {
		name: 'SkeletonBox',
		functional: true,
		props: {
			maxWidth: {
				default: 100,
				type: Number,
			},
			minWidth: {
				default: 80,
				type: Number,
			},
			height: {
				default: '1em',
				type: String,
			},
			width: {
				default: null,
				type: String,
			},
		},
		computedWidth(props) {
			return props.width || `${ Math.floor((Math.random() * (props.maxWidth - props.minWidth)) + props.minWidth) }%`;
		},
	};
</script>

<style scoped>
.skeleton-box {
  display: inline-block;
  position: relative;
  vertical-align: middle;
  overflow: hidden;
  background-color: transparent;
  border-radius: 2px;
}

.skeleton-box::after {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  transform: translateX(-100%);
  background-image: linear-gradient(
      90deg,
      rgba(200, 200, 200, 0) 0,
      rgba(200, 200, 200, 0.2) 20%,
      rgba(200, 200, 200, 0.5) 60%,
      rgba(200, 200, 200, 0)
  );
  animation: shimmer 1s infinite;
  content: '';
}

@keyframes shimmer {
  100% {
    transform: translateX(100%);
  }
}
</style>
