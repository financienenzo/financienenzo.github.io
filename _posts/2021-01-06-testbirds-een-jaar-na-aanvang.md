---
layout: post
title:  "Testbirds – één jaar na aanvang"
categories: [ Terugkijken ]
tags: [ Testbirds, Affiliate ]
image: assets/images/1.jpg
date: 2021-01-06
---

Het is inmiddels één jaar nadat ik mij heb aangemeld bij Testbirds. Testbirds is een omgeving waarbij je betaald wordt voor het testen van websites en applicaties.

Sinds mijn aanmelding heb ik 12 verschillende uitnodigingen mogen ontvangen, waarvan ik er aan 9 heb mee kunnen doen. Soms gaat het aantal mensen die mee doet met een test zo snel dat ik mij niet tijdig heb kunnen inschrijven.

## De stand na één jaar

<div class="wrapper">
    <div class="counter col_fourth">
      <i class="fa fa-code fa-2x"></i>
      <h2 class="timer count-title count-number" data-to="9" data-speed="5000"></h2>
       <p class="count-text ">Aantal onderzoeken</p>
    </div>

Zoals je kunt zien heb ik niet heel veel verschillende onderzoeken gehad en viel de tijd welke ik erin heb gestoken best mee voor de vergoeding welke er tegenover staat. De vergoeding hangt af van het aantal gevonden bugs in de tests.

Voor één test heb ik een extra vergoeding ontvangen omdat er weinig aanmelders waren en ik voor die specifieke test nog een aantal mensen wist die aan de voorwaarden voldeden. Dit is iets wat niet vaak voorkomt. Normaal gesproken krijg je enkel community punten voor het aanbrengen van nieuwe leden wat ervoor zorgt dat je mogelijk eerder uitgenodigd wordt voor nieuwe tests.

(function ($) {
	$.fn.countTo = function (options) {
		options = options || {};
		
		return $(this).each(function () {
			// set options for current element
			var settings = $.extend({}, $.fn.countTo.defaults, {
				from:            $(this).data('from'),
				to:              $(this).data('to'),
				speed:           $(this).data('speed'),
				refreshInterval: $(this).data('refresh-interval'),
				decimals:        $(this).data('decimals')
			}, options);
			
			// how many times to update the value, and how much to increment the value on each update
			var loops = Math.ceil(settings.speed / settings.refreshInterval),
				increment = (settings.to - settings.from) / loops;
			
			// references & variables that will change with each update
			var self = this,
				$self = $(this),
				loopCount = 0,
				value = settings.from,
				data = $self.data('countTo') || {};
			
			$self.data('countTo', data);
			
			// if an existing interval can be found, clear it first
			if (data.interval) {
				clearInterval(data.interval);
			}
			data.interval = setInterval(updateTimer, settings.refreshInterval);
			
			// initialize the element with the starting value
			render(value);
			
			function updateTimer() {
				value += increment;
				loopCount++;
				
				render(value);
				
				if (typeof(settings.onUpdate) == 'function') {
					settings.onUpdate.call(self, value);
				}
				
				if (loopCount >= loops) {
					// remove the interval
					$self.removeData('countTo');
					clearInterval(data.interval);
					value = settings.to;
					
					if (typeof(settings.onComplete) == 'function') {
						settings.onComplete.call(self, value);
					}
				}
			}
			
			function render(value) {
				var formattedValue = settings.formatter.call(self, value, settings);
				$self.html(formattedValue);
			}
		});
	};
	
	$.fn.countTo.defaults = {
		from: 0,               // the number the element should start at
		to: 0,                 // the number the element should end at
		speed: 1000,           // how long it should take to count between the target numbers
		refreshInterval: 100,  // how often the element should be updated
		decimals: 0,           // the number of decimal places to show
		formatter: formatter,  // handler for formatting the value before rendering
		onUpdate: null,        // callback method for every time the element is updated
		onComplete: null       // callback method for when the element finishes updating
	};
	
	function formatter(value, settings) {
		return value.toFixed(settings.decimals);
	}
}(jQuery));

jQuery(function ($) {
  // custom formatting example
  $('.count-number').data('countToOptions', {
	formatter: function (value, options) {
	  return value.toFixed(options.decimals).replace(/\B(?=(?:\d{3})+(?!\d))/g, ',');
	}
  });
  
  // start all the timers
  $('.timer').each(count);  
  
  function count(options) {
	var $this = $(this);
	options = $.extend({}, options || {}, $this.data('countToOptions') || {});
	$this.countTo(options);
  }
});
