$(document).ready(function(){
   var x = document.getElementById("map_nav");

   if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(showPos, showError);
   } else {
      var latitude = 0;
      var longitude = 0;
        // x.innerHTML = "Geolocation is not supported by this browser.";
         // x.style.display = "none";
         myNavMap(latitude, longitude);
   }

   function showPos(position){
        var latitude = position.coords.latitude;
        var longitude = position.coords.longitude;

        myNavMap(latitude, longitude);
   }

   function showError(error) {

      var latitude = 0;
      var longitude = 0;

      switch(error.code) {
       case error.PERMISSION_DENIED:
         // x.innerHTML = "User denied the request for Geolocation."
         // x.style.display = "none";
         myNavMap(latitude, longitude);
         break;
       case error.POSITION_UNAVAILABLE:
         // x.innerHTML = "Location information is unavailable."
         // x.style.display = "none";
         myNavMap(latitude, longitude);
         break;
       case error.TIMEOUT:
         // x.innerHTML = "The request to get user location timed out."
         // x.style.display = "none";
         myNavMap(latitude, longitude);
         break;
       case error.UNKNOWN_ERROR:
         // x.innerHTML = "An unknown error occurred."
         // x.style.display = "none";
         myNavMap(latitude, longitude);
         break;
      }
   }

   function myNavMap(latitude, longitude){

      var mapBoxToken = "pk.eyJ1IjoicHJvc3B0ZWFtMjAxOCIsImEiOiJjanBkZWlyMnoybHo0M3dxczh4ZGxtZG5kIn0.ycZHWnaVd_Lb2ceqYjYAqw";
      var map = L.map('map_nav');

      if(latitude !=0 || longitude !=0){
         map.setView([latitude,longitude],16);
      }else{
         $.get(location.protocol + '//nominatim.openstreetmap.org/search?format=json&q='+php_vars.address, function(data){
            map.setView([data[0].lat,data[0].lon],16);
         });

      }

      map.scrollWheelZoom.disable();

      L.tileLayer('https://a.tiles.mapbox.com/v4/mapbox.streets/{z}/{x}/{y}{r}.png?access_token=' + mapBoxToken, {
         attribution: 'Maps by <a href="https://www.mapbox.com/about/maps/">MapBox</a>. '
      }).addTo(map);

      function createButton(label, container, title, color) {
          var btn = L.DomUtil.create('button', '', container);
          btn.setAttribute('type', 'button');
          btn.setAttribute('style', 'border: 1px solid '+color+'; background: #fff; margin: 2px; padding: 2px 5px');
          btn.setAttribute('title', title);
          btn.innerHTML = label;
          return btn;
      }

      // var pathname = window.location.pathname.split( '/' );
      // var url = urlpathname[0]+'/'+pathname[1]+'/wp-content/plugins/visitor-analytics/assets/';

      var ReversablePlan = L.Routing.Plan.extend({
          createGeocoders: function() {
              var container = L.Routing.Plan.prototype.createGeocoders.call(this),
                  reverseButton = createButton('↑↓', container, 'reverse', '#3d42b4');
                  walkButton = createButton('W', container, 'walking', '#3d42b4');
                  cycleButton = createButton('C', container, 'cycling', '#3d42b4');
                  driveButton = createButton('D', container, 'driving', '#a80000');
                  nominatimButton = createButton('N', container, 'nominatim', '#a80000');
                  mapBoxButton = createButton('M', container, 'mapbox', '#3d42b4');

                  // Event to reverse the waypoints
                   L.DomEvent.on(reverseButton, 'click', function() {
                      var waypoints = this.getWaypoints();
                      this.setWaypoints(waypoints.reverse());
                      console.log("Waypoints reversed");
                   }, this);

                   // Event to switch to walking
                  L.DomEvent.on(walkButton, 'click', function() {
                     control.getRouter().options.profile = 'mapbox/walking';
                     control.route();
                     control.setWaypoints(control.getWaypoints());
                     console.log("Walking route");
                     walkButton.setAttribute('style', 'border: 1px solid #a80000; background: #fff; margin: 2px; padding: 2px 5px');
                     cycleButton.setAttribute('style', 'border: 1px solid #3d42b4; background: #fff; margin: 2px; padding: 2px 5px');
                     driveButton.setAttribute('style', 'border: 1px solid #3d42b4; background: #fff; margin: 2px; padding: 2px 5px');
                  }, this);

                  // Event to switch to cycling
                  L.DomEvent.on(cycleButton, 'click', function() {
                     control.getRouter().options.profile = 'mapbox/cycling';
                     control.route();
                     control.setWaypoints(control.getWaypoints());
                     console.log("Cycling route");
                     walkButton.setAttribute('style', 'border: 1px solid #3d42b4; background: #fff; margin: 2px; padding: 2px 5px');
                     cycleButton.setAttribute('style', 'border: 1px solid #a80000; background: #fff; margin: 2px; padding: 2px 5px');
                     driveButton.setAttribute('style', 'border: 1px solid #3d42b4; background: #fff; margin: 2px; padding: 2px 5px');
                  }, this);

                  // Event to switch to driving (default)
                  L.DomEvent.on(driveButton, 'click', function() {
                     control.getRouter().options.profile = 'mapbox/driving';
                     control.route();
                     control.setWaypoints(control.getWaypoints());
                     console.log("Driving route");
                     walkButton.setAttribute('style', 'border: 1px solid #3d42b4; background: #fff; margin: 2px; padding: 2px 5px');
                     cycleButton.setAttribute('style', 'border: 1px solid #3d42b4; background: #fff; margin: 2px; padding: 2px 5px');
                     driveButton.setAttribute('style', 'border: 1px solid #a80000; background: #fff; margin: 2px; padding: 2px 5px');
                  }, this);

                  L.DomEvent.on(nominatimButton, 'click', function() {
                      control.getPlan().options.geocoder = new L.Control.Geocoder.nominatim();
                      control.setWaypoints(control.getWaypoints());
                      console.log("Nominatim route search");
                      nominatimButton.setAttribute('style', 'border: 1px solid #a80000; background: #fff; margin: 2px; padding: 2px 5px');
                      mapBoxButton.setAttribute('style', 'border: 1px solid #3d42b4; background: #fff; margin: 2px; padding: 2px 5px');
                  }, this);

                  L.DomEvent.on(mapBoxButton, 'click', function() {
                     control.getPlan().options.geocoder = new L.Control.Geocoder.mapbox(mapBoxToken);
                     control.setWaypoints(control.getWaypoints());
                     console.log("MapBox route search");
                     mapBoxButton.setAttribute('style', 'border: 1px solid #a80000; background: #fff; margin: 2px; padding: 2px 5px');
                     nominatimButton.setAttribute('style', 'border: 1px solid #3d42b4; background: #fff; margin: 2px; padding: 2px 5px');
                  }, this);

              return container;
          }
      });

      var plan = new ReversablePlan([
         // L.latLng(latitude, longitude),
         // L.latLng(10.32, 123.92)
            // L.routing.waypoint(null, "12 Morning Star place, Auckland"),
            // L.routing.waypoint(null, "198 Dominion road, Mount Roskill, Auckland"),
      ], {
        geocoder: L.Control.Geocoder.nominatim(),
        // geocoder: L.Control.Geocoder.mapbox(mapBoxToken),
        routeWhileDragging: true
      }),
      control = L.Routing.control({
        routeWhileDragging: true,
        router: L.Routing.mapbox(mapBoxToken),
        plan: plan,
        show: true,
        collapsible: true,

      }).addTo(map);

      waypoints = [];

      var wpt = L.Routing.waypoint(L.latLng(latitude, longitude));
      waypoints.push(wpt);
      control.setWaypoints(waypoints);

      if(php_vars.address == null){
         php_vars.address = "United States";
      }

      L.Control.Geocoder.nominatim().geocode(php_vars.address, function(a, b) {
         // console.log(L.Control.Geocoder.nominatim());
         // choose the best result here. probably the first one in array
         var point = a[0];
         var wpt = L.Routing.waypoint(L.latLng(point.center.lat, point.center.lng), point.name);
         waypoints.push(wpt);
         control.setWaypoints(waypoints);
      })

      map.on('click', function(e) {
          var container = L.DomUtil.create('div'),
              startBtn = createButton('Start from this location', container, 'Start Point', '#a1a1a1'),
              destBtn = createButton('Go to this location', container, 'End Point', '#a1a1a1');

          L.popup()
              .setContent(container)
              .setLatLng(e.latlng)
              .openOn(map);

           L.DomEvent.on(startBtn, 'click', function() {
              control.spliceWaypoints(0, 1, e.latlng);
              map.closePopup();
          });

          L.DomEvent.on(destBtn, 'click', function() {
             control.spliceWaypoints(control.getWaypoints().length - 1, 1, e.latlng);
             map.closePopup();
         });
      });
   }

});
