---
layout: no-container
title: About me
permalink: /things/
---

# Photography
<div class="photo">
  <div class="thumbnail">
  </div>

  <div class="thumbnail">
  </div>

  <div class="thumbnail">
  </div>
</div>

<script type="text/javascript">
var endpoint = "https://api.flickr.com/services/rest/"
var apiKey = "4912feac8c866a2c76b84eca4bb55442";
var photosetId = "72157645448920573";
var extras = "url_sq,url_t,url_s,url_m,url_o";
var method = "flickr.photosets.getPhotos";

var request = endpoint+"?method="+method+
            "&api_key="+apiKey+
            "&photoset_id="+photosetId+
            "&extras="+extras+
            "&format=json&jsoncallback=?";
$.getJSON(request,buildGallery);

function buildGallery(data,result){
    if(result=="success"){
        var photos = data.photoset.photo;
        for(var i=0; i<photos.length; i++){
            $('<img class="thumbnail" >').attr("src",photos[i].url_m).appendTo(".photo");
        }
    }
}
</script>

# Books
