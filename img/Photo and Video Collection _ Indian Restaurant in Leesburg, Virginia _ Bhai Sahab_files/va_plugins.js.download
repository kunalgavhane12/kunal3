$(document).ready(function(){
  navigator.geolocation.getCurrentPosition(function(position) {
    setLocation(position.coords);
    },
    function(failure) {
        $.getJSON('https://ipinfo.io/geo', function(response) {
          var loc = response.loc.split(',');
          var coords = {
              latitude: loc[0],
              longitude: loc[1]
          };
          setLocation(coords);
       });
  });

   //   function get_base_url() {
   //     var url = location.href;  // entire url including querystring - also: window.location.href;
   //     var baseURL = url.substring(0, url.indexOf('/', 14));
   //
   //     if (baseURL.indexOf('http://localhost') != -1) {
   //         // Base Url for localhost
   //         var url = location.href;  // window.location.href;
   //         var pathname = location.pathname;  // window.location.pathname;
   //         var index1 = url.indexOf(pathname);
   //         var index2 = url.indexOf("/", index1 + 1);
   //         var baseLocalUrl = url.substr(0, index2);
   //
   //         return baseLocalUrl + "/";
   //     }
   // 	else if(baseURL.match(/[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}/))
   // 	{
   // 	    // Base Url for localhost
   //         var url = location.href;  // window.location.href;
   //         var pathname = location.pathname;  // window.location.pathname;
   //         var index1 = url.indexOf(pathname);
   //         var index2 = url.indexOf("/", index1 + 1);
   //         var baseLocalUrl = url.substr(0, index2);
   //
   //         return baseLocalUrl + "/";
   //
   // 	}
   //     else {
   //         // Root Url for domain name
   //         return baseURL + "/";
   //     }
   // }

    function setLocation(position){
      var lati = position.latitude;
      var longi = position.longitude;
      var pathname = window.location.pathname.split( '/' );

      Cookies.set('latitude',lati);
      Cookies.set('longitude',longi);

       $.getJSON('https://ipinfo.io/geo',function(data){
         var url = va_plugin_url+'/visitor-analytics/includes/counter/counter.php?page=counter';

         $.ajax({
             url     :   url,
             type    :  "POST",
             data    :   data,
             // success : function(e){
             //   alert(e);
             // }
         })
       });
     }

});
