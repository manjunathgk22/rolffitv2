<script lang="ts">
  import { onMount } from "svelte";
  import { homeAnchor, loadPagePromise, slickScrollInstance } from "../store";
  import anime from "animejs";
  import { loadImage } from "../utils";

  let homeContainer; // Container
  let backgroundContainer, backgroundImage; // Offsets
  let path1, path2, path3, path4; // SVG Paths
  let titleWord1, titleWord2, shortDetails, callToAction; // Elements for animations

  onMount(async () => {
    await loadPagePromise;
    $homeAnchor = homeContainer;

    // Add scroll offsets to slickScroll
    $slickScrollInstance.addOffset({
      element: backgroundContainer,
      speedY: 0.8,
    });

    introAnimation();
  });

  // Page load animations
  function introAnimation() {
    let animation = [{ strokeDashoffset: "0" }];

    // Signature animation using svg strokDashOffset
    // path1.animate(animation, {
    //   duration: 1000,
    //   delay: 500,
    //   easing: "cubic-bezier(.72,.3,.25,1)",
    //   fill: "forwards",
    // });
    // path2.animate(animation, {
    //   duration: 300,
    //   delay: 1500,
    //   easing: "cubic-bezier(.47,.41,.26,1)",
    //   fill: "forwards",
    // });
    // path3.animate(animation, {
    //   duration: 200,
    //   delay: 1800,
    //   easing: "cubic-bezier(.47,.41,.26,1)",
    //   fill: "forwards",
    // });
    // path4.animate(animation, {
    //   duration: 1000,
    //   delay: 2000,
    //   easing: "cubic-bezier(.47,.41,.26,1)",
    //   fill: "forwards",
    // });

    // Animate background image
    Object.assign(backgroundContainer.style, {
      height: "0",
      transform: "scale(1.3)",
    });
    backgroundImage.style.transform = "translateY(80%) scale(1.4)";

    anime({
      targets: backgroundContainer,
      height: "100%",
      scale: 1,
      easing: "cubicBezier(0.165, 0.84, 0.44, 1)",
      duration: 1500,
      delay: 1000,
      complete: () => {
        backgroundContainer.style.boxShadow = "3px 9px 18px rgba(0, 0, 0, 0.2)";
      },
    });
    anime({
      targets: backgroundImage,
      translateY: "0",
      scale: 1,
      easing: "cubicBezier(0.165, 0.84, 0.44, 1)",
      duration: 1500,
      delay: 1000,
    });

    // Animate title
    let titleElems = [titleWord1, titleWord2, shortDetails, callToAction];
    titleElems.forEach((e) => {
      e.style.transform = "translateY(-150%) rotate(-8deg)";
    });
    anime({
      targets: titleElems,
      rotate: "0",
      translateY: "0%",
      easing: "cubicBezier(0.165, 0.84, 0.44, 1)",
      duration: 1400,
      delay: anime.stagger(80, { start: 2000 }),
    });
  }
</script>

<div id="content-container" style="padding-top: 23vh" bind:this={homeContainer}>
  <div class="content-wrapper">
    <div class="flex">
      <div class="flex-wrapper first">
        <svg id="signature" class="h-signature" viewBox="0 0 190 277">
          <g>
            <path
              bind:this={path1}
              class="path-1"
              style="fill:none;stroke:#ffffff;stroke-width:2.5;stroke-linecap:round;stroke-linejoin:miter;stroke-opacity:1;stroke-miterlimit:4;"
              d="M436.35,298.74c0.47-0.29,0.94-0.58,1.41-0.87c1.43,2.11,3.08,4.11,4.25,6.36c11.55,22.21,23.43,44.25,34.41,66.73  c19.15,39.22,37.91,78.67,49.31,121.04c3.7,13.76,7.72,27.76,2.31,41.55c16.14,18.56,32.05,36.85,48.82,56.13  c7.68-12.95,9.39-26.03,10.79-39.32c2.87-27.41-6.7-52.35-15.77-77.12c-11.68-31.91-24.47-63.43-37.49-94.83  c-11.31-27.27-23.05-54.39-35.69-81.06c-7.95-16.77-17.91-32.59-26.95-48.84c-3.17-5.7-6.51-6.04-10.06-0.38  c-2.76,4.4-5.79,8.66-8.14,13.27c-13.96,27.4-28.58,54.5-41.33,82.45c-9.32,20.43-16.2,41.98-23.89,63.14  c-1.05,2.9-0.5,6.38-0.74,10.41c41.41-2.34,80.93-0.11,115.59,24.63c0.77-0.56,1.55-1.12,2.32-1.68  C482.46,393.16,459.41,345.95,436.35,298.74z M796.78,240.82c-3.23,4.06-5.25,5.98-6.52,8.32c-9.78,17.92-19.51,35.88-29.07,53.92  c-7.56,14.25-15.88,28.23-21.96,43.1c-4.91,12-5.86,25.6-10.53,37.73c-14.11,36.64-29.43,72.82-43.8,109.36  c-11.43,29.08-13.06,58.74-2.92,88.62c0.8,2.36,2.79,4.31,4.23,6.45c1.81-1.33,3.94-2.39,5.39-4.04  c13.09-14.88,26.14-29.81,38.99-44.9c2.04-2.4,4.61-5.91,4.25-8.54c-2.77-20.16,3.28-38.8,9.55-57.25  c19.29-56.81,46.37-110.13,74.96-162.65c6.45-11.85,8.93-21.06,0.16-32.76C811.18,267.11,804.95,254.47,796.78,240.82z   M662.15,262.77c-0.94-0.56-1.88-1.13-2.82-1.69c1.35-3.13,2.36-6.46,4.11-9.35c7.27-12,15.38-23.54,22.04-35.86  c9.38-17.37,18.15-35.11,26.42-53.04c7.83-16.99,2.28-30.92-11.06-43.12c-16.43-15.02-32.15-30.82-48.43-46.01  c-2.62-2.45-6.59-3.45-9.94-5.12c-0.78,3.41-2.26,6.82-2.24,10.22c0.1,25.93,0.71,51.87,0.73,77.8c0.02,26.85-0.53,53.7-0.55,80.55  c0,3.5,1.6,7.01,2.59,10.49c4.01,14.14,17.11,18.75,27.58,26.06c18.21,12.72,36.78,24.95,54.65,38.13c8.42,6.21,9.13,6.77,14.12-2.4  c9.93-18.21,19.91-36.39,29.82-54.61c4.43-8.14,8.72-16.35,13.59-25.49c-3.4-0.51-5.15-1.16-6.79-0.97  c-24.23,2.87-48.66,4.73-72.6,9.19C687.21,240.57,668.43,241.63,662.15,262.77z M480.31,227.71c0.57,2.59,0.57,3.88,1.11,4.86  c14.32,26.23,28.65,52.46,43.09,78.63c3.43,6.22,7.17,5.1,12.57,1.28c20.83-14.7,41.59-29.62,63.4-42.75  c14.46-8.7,21.81-20.81,22.36-36.42c1.01-28.3,0.43-56.65,0.5-84.98c0.05-23.18,0.22-46.36-0.03-69.54  c-0.04-3.5-2.01-6.97-3.09-10.46c-3.41,1.51-7.57,2.22-10.11,4.65c-16.55,15.8-32.24,32.56-49.27,47.81  c-9.84,8.81-11.27,18.29-9.12,30.24c4.26,23.73,15.85,44.02,28.43,63.96c7.98,12.64,15.85,25.36,23.57,38.16  c1.47,2.44,2.02,5.42,3,8.16c-12.97-14.73-12.89-14.98-22.29-18.12C551.05,232.06,516.32,230.09,480.31,227.71z M822.2,634.08  c16.78-12.52,28.5-27.09,38.94-42.96c3.71-5.64,2.58-8.35-3.01-11.31c-14.57-7.72-29.85-14.56-43.11-24.16  c-17.49-12.66-34.73-12.63-54.07-6.17c-12.91,4.32-25.63,8.41-34.94,18.78c-7.94,8.85-15.04,18.45-22.84,27.45  c-5.36,6.19-3.74,10.78,3.58,11.37c11.73,0.94,23.61,0.27,35.42,0.05c18.31-0.34,36.63-1.53,54.91-1.1  c13.43,0.32,19.63,6.58,23,19.57C820.68,627.86,821.22,630.13,822.2,634.08z M440.92,633.18c10.02-26.83,11.53-28.15,41.14-27.7  c15.23,0.23,30.43,2.31,45.67,2.65c10.18,0.22,20.46-0.69,30.59-1.97c7.12-0.9,6.28-5.19,2.49-9.64  c-3.76-4.41-8.06-8.49-11.09-13.36c-13.53-21.81-33.54-32.9-58.37-36.51c-3.31-0.48-6.54-1.95-9.83-2.04  c-3.7-0.1-7.96-0.14-11.07,1.5c-17.51,9.23-34.77,18.96-52.09,28.56c-6.31,3.5-12.56,7.13-18.72,10.63  C407.1,602.65,428.79,627.8,440.92,633.18z M876.22,417.3c-7.46-36.77-35.82-107.11-47.27-116.87c-25,45.97-48.6,92.36-69.45,143.09  C796.11,417.25,835.42,415.25,876.22,417.3z M525.97,529.81c0-7.05,1.17-13.56-0.23-19.45c-3.79-15.99-8.83-31.69-13.04-47.59  c-2.34-8.85-7.8-14.98-15.16-19.86c-32.6-21.62-68.94-24.58-106.5-21.19c-1.99,0.18-5.02,2.02-5.38,3.59  c-0.39,1.75,1.18,4.77,2.83,6.01c5.6,4.21,11.6,7.88,17.46,11.74c17.82,11.72,36.12,22.76,53.34,35.3  C481.45,494.47,502.73,511.78,525.97,529.81z M745.3,547.67c42.35-7.25,85.43-14.99,128.66-21.76c9.13-1.43,12.24-5.59,12.02-13.57  c-0.52-19.18-1.28-38.36-2.17-57.53c-0.11-2.43-1.64-4.8-2.86-8.14C832.34,478.13,784.21,507.85,745.3,547.67z M517.26,548.59  c-4.69-5.17-7.65-9.07-11.22-12.3c-36.33-32.79-76.86-59.78-118.25-85.61c-6.62-4.13-9.16-1.45-9.29,4.91  c-0.45,20.41-0.48,40.83-0.81,61.24c-0.09,5.79,2.53,7.56,8.16,8.33c23.25,3.15,46.49,6.49,69.59,10.59  C475.45,539.31,495.25,543.98,517.26,548.59z M737.27,527.24c1.09,0.49,2.18,0.97,3.27,1.46c2.24-1.89,4.43-3.85,6.73-5.66  c21.84-17.11,43.18-34.93,65.72-51.08c19.28-13.81,40.02-25.57,59.9-38.57c2.35-1.53,4.29-5.06,4.52-7.82  c0.11-1.27-4.3-4.05-6.8-4.24c-34.34-2.59-67.75,0.31-98.38,18.08c-10.37,6.02-18.29,13.86-21.44,26.04  c-3.05,11.79-7.49,23.25-10.23,35.1C738.57,509.23,738.31,518.33,737.27,527.24z M623.05,299c-0.32-5.23-0.42-8.28-0.7-11.32  c-0.84-9.06-2.87-10.29-10.84-5.97c-6.94,3.76-14.24,7.2-20.3,12.13c-13.38,10.88-26.52,22.16-38.71,34.33  c-2.87,2.86-3.46,10.57-1.88,14.85c4.54,12.21,9.41,24.7,16.64,35.4c7.68,11.36,17.61,21.46,27.75,30.82  c5.83,5.38,13.74,2.23,17.48-3.78c2.57-4.13,4.02-12.36,1.65-15.57c-10.43-14.16-9.23-30.76-11.38-46.47  c-1.46-10.68,0.66-22.45,10.93-28.3C621.83,310.49,624.68,305.39,623.05,299z M714.25,337.68c-1.06-2.45-1.64-5.29-3.25-7.29  c-17.4-21.63-37.77-39.58-63.75-50.37c-4-1.66-6.6-0.81-6.76,4c-0.12,3.66,0.15,7.36-0.25,10.98c-1.02,9.16,1.1,15.87,9.66,21.54  c4.84,3.21,9.16,10.94,9.34,16.77c0.58,18.76,1.53,38-9.95,54.81c-4.37,6.39-3.66,12.93,1.71,18.37c5.74,5.81,12.62,5.76,19.26,1.66  c3.59-2.22,6.84-5.15,9.84-8.16c14.07-14.13,22.07-31.96,29.86-49.87C711.63,346.24,712.73,342.11,714.25,337.68z M546.58,138.52  c-0.88-0.39-1.75-0.78-2.63-1.17c-21.88,27.98-43.77,55.96-65.81,84.14c39.23,5.8,76.04,11.25,112.59,16.65  C571.7,208.09,548.55,178,546.58,138.52z M783.1,221.9c-17.57-29.08-39.89-54.02-63.28-81.24c-3.84,39.92-25.99,68.77-44.21,97.62  C711.07,232.88,746.2,227.52,783.1,221.9z M466.44,543.2c0.09-0.76,0.18-1.53,0.27-2.29c-28.98-4.4-57.96-8.8-89.69-13.61  c6.7,19.94,12.41,36.95,18.5,55.05C420.75,568.41,443.6,555.8,466.44,543.2z M799.19,540.81c-0.08,0.72-0.16,1.44-0.24,2.16  c22.21,12.25,44.42,24.51,67.6,37.3c9.02-16.76,14.22-33.1,16.75-52.4C854.06,532.37,826.62,536.59,799.19,540.81z"
            />
            <!-- <path bind:this={path2} class="path-2" style="fill:none;stroke:#ffffff;stroke-width:2.5;stroke-linecap:round;stroke-linejoin:miter;stroke-opacity:1;stroke-miterlimit:4;" d="m 132.18539,124.21348 -23.91573,78.79214" />
            <path bind:this={path3} class="path-3" style="fill:none;stroke:#ffffff;stroke-width:2.5;stroke-linecap:round;stroke-linejoin:miter;stroke-opacity:1;stroke-miterlimit:4;" d="m 110.30899,131.25842 c 0,0 -0.74157,11.67978 -2.7809,17.98315 -2.03933,6.30337 -6.67416,20.20787 -6.85955,24.10112" />
            <path
              bind:this={path4}
              class="path-4"
              style="fill:none;stroke:#ffffff;stroke-width:2.5;stroke-linecap:round;stroke-linejoin:miter;stroke-opacity:1;stroke-miterlimit:4;"
              d="m 121.98876,150.35393 c 0,0 -5.93258,-7.97191 -17.05618,-6.67416 -11.123592,1.29776 -20.207862,11.30899 -21.134827,12.60675 -0.926968,1.29775 -10.011238,9.64044 2.224717,15.01685 12.235955,5.3764 38.93259,-7.23034 38.93259,-7.23034 0,0 17.79775,-10.01123 18.91011,-10.01123 1.11236,0 -4.63483,5.93258 -4.26405,7.23033 0.37079,1.29776 2.77483,2.03165 7.23034,-1.48314 0.97548,-0.76952 17.21937,-0.82644 22.21274,0.97637 1.8694,0.67493 3.48943,-0.21536 4.98153,-1.37648 0.97963,-0.76233 9.43868,2.03194 9.43868,2.03194"
            /> -->
          </g>
        </svg>
      </div>

      <div class="flex-wrapper second">
        <h1 class="title">
          <div class="title-mask">
            <div class="word" bind:this={titleWord1}>ROLF</div>
          </div>
          <br />
          <div class="title-mask">
            <div class="word" bind:this={titleWord2}>FIT</div>
          </div>
        </h1>
        <div class="occupation mask">
          <p class="paragraph" bind:this={shortDetails}>Introducing Massage Therapy</p>
        </div>
        <div class="wrapper action-mask">
          <div class="action" bind:this={callToAction}>
            <div class="mask">
              {#await loadImage("assets/imgs/scroll_arrow.png") then src}
                <img {src} alt="" />
              {/await}
            </div>
            <div>scroll</div>
          </div>
        </div>
      </div>

      <div class="parallax-wrapper home-back" bind:this={backgroundContainer}>
        {#await loadImage("assets/imgs/home-back.jpg") then src}
          <img {src} bind:this={backgroundImage} draggable="false" alt="Home Background" style="width:100%; height: 100%; object-fit: cover;" />
        {/await}
      </div>
    </div>
  </div>
</div>

<style lang="sass">

@import "../consts.sass"
@include textStyles()

#content-container
	height: 100vh
	width: 100vw
	padding: 12vh 7vw
	box-sizing: border-box
	position: relative

	.content-wrapper
		position: relative
		height: 100%
		box-sizing: border-box
		z-index: 2

	.flex
		z-index: 2
		width: 95%
		height: 100%
		display: flex
		flex-direction: row
		justify-content: space-between
		position: relative
		box-sizing: border-box

		.flex-wrapper
			position: relative
			height: 100%
			display: flex
			flex-direction: column
			justify-content: center

			&.second
				margin-right: 5vw 
				justify-content: flex-end

			h1
				font-weight: 400

			.title-mask
				overflow: hidden
				display: inline-flex

			.mask
				overflow: hidden

			.h-signature
				width: 35vh
				margin-left: -6vh

			.occupation
				position: relative
				margin-top: 8vh

			.action-mask
				margin-top: 10vh
				margin-right: 7vw
				display: inline-flex
				overflow: hidden

				.action
					font-size: 2vh
					letter-spacing: 0.5vh
					font-family: $font
					text-transform: uppercase
					color: white
					position: relative
					display: inline-flex
					flex-direction: row
					align-items: center

					.mask
						overflow: hidden
						height: 2vh

						img
							height: 2.3vh
							margin-right: 1.5vh
							animation: scrollArrowLoop 3s ease infinite

	.parallax-wrapper
		position: absolute
		left: 0
		z-index: -1
		width: 80%
		height: 100%
		margin-left: 5%
		border-radius: 1.5vh
		overflow: hidden
		box-sizing: border-box
		-webkit-touch-callout: none
		-webkit-user-select: none
		-moz-user-select: none
		-ms-user-select: none
		user-select: none
		transition: box-shadow 0.6s ease
		-webkit-transition: box-shadow 0.6s ease

		@media only screen and (max-width: 1250px)
			&
				opacity: 0.7

		@media only screen and (max-width: 750px)
			&
				opacity: 0.3

		img
			height: 100%
			width: 100%
			object-fit: cover
			border-radius: 1.5vh

@media only screen and (min-width: 1250px)
	.h-signature
		display: block

	.occupation
		width: 100%

	#content-container .flex *
		text-align: left

@media only screen and (max-width: 1250px)
	#content-container .flex *
		text-align: left

	.flex
		justify-content: center !important
		width: 100% !important

		.flex-wrapper 
			&.first
				display: none !important

			&.second
				justify-content: center !important
				margin: 0

	#content-container .flex .bottom
		text-align: left
		left: 5vw

	.parallax-wrapper
		width: 100% !important
		margin-left: 0 !important

@media only screen and (max-width: 750px)
	.occupation
		width: 70%


#signature
	.path-1
		stroke-dasharray: 365
		stroke-dashoffset: 365
	
	.path-2
		stroke-dasharray: 85
		stroke-dashoffset: 85

	.path-3
		stroke-dasharray: 45
		stroke-dashoffset: 45

	.path-4
		stroke-dasharray: 180
		stroke-dashoffset: 180


@keyframes scrollArrowLoop
	0%
		transform: translateY(-120%)
	
	30%
		transform: translateY(0%)
	
	70%
		transform: translateY(0%)
	
	100%
		transform: translateY(120%)

</style>
