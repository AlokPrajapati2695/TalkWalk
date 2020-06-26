// Front end JS additions / updates

// HERO RESPONSIVE IMAGE CHANGES
// watch window sizes
// media query event handler
if($('.tw-hero:not(".home-hero")')){
	var resize = function() {

		var screenWidth = parseInt($('body').width());

		if (screenWidth < 600) {
			console.log('mobile')
			if ($(".tw-hero-bg").is('[data-bg-mobile]')) {
				$(".tw-hero-bg").css('background-image', function () {
					var bg = ('url(' + $(this).data("bg-mobile") + ')');
					return bg;
				});
			}
		}
		else if (screenWidth < 1024) {
			console.log('tablet')
			if ($(".tw-hero-bg").is('[data-bg-tablet]')) {
				$(".tw-hero-bg").css('background-image', function () {
					var bg = ('url(' + $(this).data("bg-tablet") + ')');
					return bg;
				});
			}
		}
		else {
			console.log('desktop')
			if ($(".tw-hero-bg").is('[data-bg-desktop]')) {
				$(".tw-hero-bg").css('background-image', function () {
					var bg = ('url(' + $(this).data("bg-desktop") + ')');
					return bg;
				});
			}
		}
	}

	// create timeout check for the window resizing
	var rtime;
	var timeout = false;
	var delta = 200;
	$(window).resize(function() {
		rtime = new Date();
		if (timeout === false) {
			timeout = true;
			setTimeout(resizeend, delta);
		}
	});

	function resizeend() {
		if (new Date() - rtime < delta) {
			setTimeout(resizeend, delta);
		} else {
			timeout = false;
			//alert('Done resizing');
			resize();
		}
	}
}


$(document).ready(function(){

	// Overriding language open / close
	$(".actual-lang").on("click", function() {
		console.log('yes')
		$('.tw-nav .nav-shorts').addClass('has-background');
	});

	$(".overlay-close").on("click", function() {
		$('.tw-nav .nav-shorts').removeClass('has-background');
	});


	// resize event for hero image changes
	if($('.tw-hero:not(".home-hero")')){
		resize();
	}


	// content fade in on scroll
	inView.threshold(0.1);

	inView('.tw-block, .tw-hero').on('enter', function(el){
		$(el).addClass('animateIn');
	});

	// HOMEPAGE HERO
	if($('.front-page-hero').length >0 ){

		// HOMEPAGE HERO
		function fullPage() {

			var transitionSpeed = 1500;

			$('#fullpage').fullpage({
				autoScrolling: true,
				fitToSection: true,
				scrollingSpeed: transitionSpeed,

				afterRender: function() {
					console.log("FullPage Rendered");
					$('.tw-fp .section').toggleClass('fpRendered');
				},

				onLeave: function(origin, destination, direction) {
					// Toggles a class for handling the second section's rotating messages
					if ( destination.index == 1 ) {
						$('#sectionTwo').addClass('fpRotateMessaging');
					} else {
						setTimeout( function() {
							$('#sectionTwo').removeClass('fpRotateMessaging');
						}, transitionSpeed )
					}

					// Toggles a class to break-out of FullPage.js restrictions if it's the last slide
					if ( destination.isLast ) {
						setTimeout( function() {
							$('html').addClass('fp-scroll-free');
						}, transitionSpeed );
					}

					// Toggles classes & reactivates FullPage.js if scrolling up from the last slide
					// We check the scroll position so that it only fires if we're 1 scroll from the top
					var scroll = $(window).scrollTop();
					if ( scroll < 101 ) {
						if ( origin.isLast && direction == 'up' ) {
							setTimeout( function() {
								$('html').removeClass('fp-scroll-free');
							}, (transitionSpeed / 2) );
						}
					} else if ( origin.isLast && direction == 'up' ) {
						// Returning false tells FullPage.js to do nothing
						return false;
					} else {
						return false;
					}
				},

				afterResize: function(width) {
					if ( width < 1024 ) {
						$.fn.fullpage.setAutoScrolling(false);
						$.fn.fullpage.setFitToSection(false);
						$('html').addClass('fp-scroll-free');
					}
					if ( width >= 1024 ) {
						$.fn.fullpage.setAutoScrolling(true);
						$.fn.fullpage.setFitToSection(true);
						$('html').removeClass('fp-scroll-free');
					}
				},
			});
		}
		if ( window.innerWidth >= 1024 ) {
			// Double check the windows size before firing the function for performance reasons
			fullPage();
		}

		function sectionTwoInView() {
			// Adds a class to apply animations to the second section on smaller devices
			// - Uses the existing inView library
			var target = $('#sectionTwo');
			if ( window.innerWidth < 1024 ) {
				inView('#sectionTwo').once('enter', function(el) {
					$(target).addClass('fpRotateMessaging');
					console.log("Section 2 is visible.");
				});
			}
		}
		sectionTwoInView();

	} // endif home hero

	// Track mouse movement over buttons for hover effect
	const hoverBtn = $('.tw-button');

	hoverBtn.each(function(){
		const hoverBtnBG = $(this).find('.tw-button-bg');
		$(this).mousemove(function(e){
			const offset = $(this).offset();
			relX = event.pageX- offset.left;
			relY = event.pageY- offset.top;
			hoverBtnBG.css({
				top: relY + 'px',
				left: relX + 'px'
			});
		});
	});


	// Overriding nav dropdown opening
	// so we can add a class to the main nav bar to change the background colour
	$(".navbar-desktop .navbar-nav > LI").each(function(e,t){
		var n = $(t);
		n.on("mouseenter", function(){
			n.addClass("open"),
			$(".navbar-desktop .navbar-collapse, navbar-collapse.in").addClass("no-overflow");
			$('.tw-nav .navbar-desktop .navbar-default').addClass('has-background');
			$('.tw-nav .nav-shorts').addClass('has-background');
		}),
		n.on("mouseleave",function(){
			n.removeClass("open"),
			$(".navbar-desktop .navbar-collapse, navbar-collapse.in").removeClass("no-overflow");
			$('.tw-nav .navbar-desktop .navbar-default').removeClass('has-background');
			$('.tw-nav .nav-shorts').removeClass('has-background');
		});
	});


	// Overriding mobile menu toggle to animate X
	// and add class for background
	$('.navbar-toggle').on('click', function(){
		$(this).toggleClass('collapsed');
		$('.tw-nav .navbar-default').toggleClass('has-background mobile-nav-open');
		$('.tw-nav .nav-shorts').toggleClass('has-background');
	});

	$('.navbar.navbar-mobile .dropdown-toggle').each(function(){
		$(this).on('click', function(){
			$('.navbar.navbar-mobile ul.collapse').collapse('hide');
			$(this).collapse();
		});
	});


	// Enterprise carousel
	$(document).on('click', '#enterprise-slide1', function(){
		$('.tw-enterprise-carousel .carousel').carousel(0)
	});
	$(document).on('click', '#enterprise-slide2', function(){
		$('.tw-enterprise-carousel .carousel').carousel(1)
	});
	$(document).on('click', '#enterprise-slide3', function(){
		$('.tw-enterprise-carousel .carousel').carousel(2)
	});
	$(document).on('click', '#enterprise-slide4', function(){
		$('.tw-enterprise-carousel .carousel').carousel(3)
	});

	// Match up custom indicators with boostrap carousel indicators
	$('#tw-enterprise-carousel').on('slid.bs.carousel', function() {
		$(".carousel-title-links li").removeClass("active");
		var indicators = $("#tw-enterprise-carousel .carousel-indicators li.active").data("slide-to");
		var a = $(".carousel-title-links").find("[data-slide-to='" + indicators + "']").addClass("active");
	});

	/*$(document).on('click', '.tw-hero-indicator', function(e){
		e.preventDefault();
		$('html, body').animate({
			scrollTop: $(".tw-content").offset().top - 100
		}, 1000);
	});*/

});