<script lang="ts">
	import { Color } from '$shared/enums/color';
	import { IconSize } from '$shared/enums/iconSize';

	export let size: IconSize = IconSize.Medium;
	export let color: Color | string = Color.Primary;
	export let disabled = false;

	let colorValue: string;
	switch (color) {
		case Color.Accent:
			colorValue = 'var(--accent-color)';
			break;
		case Color.Tertiary:
			colorValue = 'var(--divider-color)';
			break;
		case Color.Secondary:
			colorValue = 'var(--secondary-text-color)';
			break;
		case Color.Primary:
			colorValue = 'var(--text-color)';
			break;
		default:
			colorValue = color;
			break;
	}
</script>

<div class="root" class:disabled style={`color: ${colorValue}; font-size: ${size}px;`}>
	<slot />
</div>

<style>
	.root {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	.disabled {
		opacity: 0.2;
	}
</style>
