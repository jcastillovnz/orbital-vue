<template>
  <div >

<div   align="center" class="threesixty-wrapper">


<div  class="threesixty" id="{index}" data-path="/src/assets/img/rdc/renders/{index}.jpg" data-count="31">


</div>

</div>
<br>


<div class="btn-group btn-group-justified" > 


<div class="controller"> 

<!--  
 <div class="control play icon-play" value="play" id="control-play"> </div>
-->
  
<div class="control prev controls in" id="control-left"> 
</div> 
<div class="control next" id="control-right"> 
</div>
</div> 

<div class="controller"> 
<div class="control"  id="control-zoom-out"> 
</div> 
<div class="control"   id="control-zoom-in"> 
</div> 
</div> 

</div>




<!-- LOADER -->

<!-- LOADER -->



  </div>
</template>

<script>
export default {
  mounted() {



$(document).ready(function(){
(function ( $, window, document, undefined ) {


var scope,
    pluginName = 'threeSixty',
    defaults = {
        dragDirection: 'horizontal',
        useKeys: false,
        draggable: true
    },
    dragDirections = ['horizontal', 'vertical'],
    options = {},
    $el = {},
    data = [],
    total = 0,
    loaded = 0;

    /**
     * Constructor
     * @param {jQuery Object} element       main jQuery object
     * @param {Object} customOptions        options to override defaults
     */
    function ThreeSixty( element, customOptions ) {
        scope = this;
        this.element = element;
        options = options = $.extend( {}, defaults, customOptions) ;
        this._defaults = defaults;
        this._name = pluginName;

        // make sure string input for drag direction is valid
        if($.inArray(options.dragDirection, dragDirections) < 0){
            options.dragDirection = defaults.dragDirection;
        }

        this.init();
    }

    // PUBLIC API -----------------------------------------------------

    $.fn.destroy = ThreeSixty.prototype.destroy = function(){
        if(options.useKeys === true) $(document).unbind('keydown', this.onKeyDown);
        $(this).removeData();
        $el.html('');
    };

    $.fn.nextFrame = ThreeSixty.prototype.nextFrame = function(){
        $(this).each(function(i){
            var $this = $(this),
                val = $this.data('lastVal') || 0,
                thisTotal = $this.data('count');

            val = val + 1;

            $this.data('lastVal', val);

            if(val >= thisTotal) val = val % (thisTotal - 1);
            else if(val <= -thisTotal) val = val % (thisTotal - 1);
            if(val > 0) val = thisTotal - val;

            val = Math.abs(val);
            $this.find('.threesixty-frame').css({visibility: 'hidden'});
            $this.find('.threesixty-frame:eq(' + val + ')').css({ visibility: 'visible'}).css({display: 'block'});
            $this.find('.masks').css({visibility: 'hidden'}).attr("id","false");
            $this.find('.masks:eq(' + val + ')').css({display: 'block'}).css({ visibility: 'visible'}).attr("id","true");
            $this.find('.highlights').css({display: 'none'}).css({visibility: 'hidden'});
            canvas();

        });
    };

    $.fn.prevFrame = ThreeSixty.prototype.prevFrame = function(){
        $(this).each(function(i){
            var $this = $(this),
                val = $this.data('lastVal') || 0,
                thisTotal = $this.data('count');

            val = val - 1;

            $this.data('lastVal', val);

            if(val >= thisTotal) val = val % (thisTotal - 1);
            else if(val <= -thisTotal) val = val % (thisTotal - 1);
            if(val > 0) val = thisTotal - val;

            val = Math.abs(val);
            $this.find('.threesixty-frame').css({visibility: 'hidden'});
            $this.find('.threesixty-frame:eq(' + val + ')').css({ visibility: 'visible'}).css({display: 'block'});
            $this.find('.masks').css({visibility: 'hidden'}).attr("id","false");
            $this.find('.masks:eq(' + val + ')').css({display: 'block'}).css({ visibility: 'visible'}).attr("id","true");
            $this.find('.highlights').css({display: 'none'}).css({visibility: 'hidden'});
            canvas();

        });
    };

    // PRIVATE METHODS -------------------------------------------------

    /**
     * Initializiation, called once from constructor
     * @return null
     */
    ThreeSixty.prototype.init = function () {
        var $this = $(this.element);

        // setup main container
        $el = $this;

        // store data attributes for each 360
        $this.each(function(){
            var $this = $(this),
                path = $this.data('path'),
                count = $this.data('count');
            data.push({'path': path, 'count': count, 'loaded': 0, '$el': $this});
            total += count;
        });

        _disableTextSelectAndDragIE8();

        this.initLoad();
    };

    /**
     * Start loading all images
     * @return null
     */
    ThreeSixty.prototype.initLoad = function() {
        var i = 0, len = data.length, url, j;
        $el.addClass('preloading');
        for(i; i < len; i++){
            j = 0;
            for(j; j < data[i].count; j++){
                url = data[i].path.replace('{index}', j);
                $('<img/>').data('index', i).attr('src', url).load(this.onLoadComplete);
            }
        }
    };

ThreeSixty.prototype.onLoadComplete = function(e) {
var index = $(e.currentTarget).data('index'),
thisObj = data[index];
thisObj.loaded++;
if(thisObj.loaded === thisObj.count){
scope.onLoadAllComplete(index);
}
};

ThreeSixty.prototype.onLoadAllComplete = function(objIndex) {
var $this = data[objIndex].$el,
html = '',
l = data[objIndex].count,
pathTemplate = data[objIndex].path,
i = 0;
// remove preloader
$this.html('');
$this.removeClass('preloading');
// add 360 images
for(i; i < l; i++){
var display = (i === 0) ? 'visible' : 'hidden';
var none = 'hidden'

var path_masks="/src/assets/img/rdc/masks/"



var path_highlights_B01="/src/assets/img/rdc/highlights/B01/"
var path_highlights_B02="/src/assets/img/rdc/highlights/B02/"
var path_highlights_B03="/src/assets/img/rdc/highlights/B03/"
var path_highlights_B04="/src/assets/img/rdc/highlights/B04/"
var path_highlights_B05="/src/assets/img/rdc/highlights/B05/"
var path_highlights_B06="/src/assets/img/rdc/highlights/B06/"
var path_highlights_B07="/src/assets/img/rdc/highlights/B07/"
var path_highlights_B08="/src/assets/img/rdc/highlights/B08/"
var path_highlights_B09="/src/assets/img/rdc/highlights/B09/"




var extencion=".png"
html += '<img class="threesixty-frame renders" style="visibility:' +display + ';" data-index="' + i + '"  id="' + i + '" src="' + pathTemplate.replace('{index}', i) + '"/>';
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
html += '<img class="masks center" alt="'+i+'" crossOrigin = "Anonymous"  style="visibility:' + display + ';" id="true"     data-index="' + i + '"   src="' + path_masks+''+i+extencion+'"/>';

html += '<img class="highlights center"     style="visibility:' + none + ';" data-index="' + i + '"  id="highlights_B01_' + i + '" src="' + path_highlights_B01+''+i+extencion+'"/>';
html += '<img class="highlights center"     style="visibility:' + none + ';" data-index="' + i + '"  id="highlights_B02_' + i + '" src="' + path_highlights_B02+''+i+extencion+'"/>';
html += '<img class="highlights center"     style="visibility:' + none + ';" data-index="' + i + '"  id="highlights_B03_' + i + '" src="' + path_highlights_B03+''+i+extencion+'"/>';
html += '<img class="highlights center"     style="visibility:' + none + ';" data-index="' + i + '"  id="highlights_B04_' + i + '" src="' + path_highlights_B04+''+i+extencion+'"/>';
html += '<img class="highlights center"     style="visibility:' + none + ';" data-index="' + i + '"  id="highlights_B05_' + i + '" src="' + path_highlights_B05+''+i+extencion+'"/>';
html += '<img class="highlights center"     style="visibility:' + none + ';" data-index="' + i + '"  id="highlights_B06_' + i + '" src="' + path_highlights_B06+''+i+extencion+'"/>';
html += '<img class="highlights center"     style="visibility:' + none + ';" data-index="' + i + '"  id="highlights_B07_' + i + '" src="' + path_highlights_B07+''+i+extencion+'"/>';
html += '<img class="highlights center"     style="visibility:' + none + ';" data-index="' + i + '"  id="highlights_B08_' + i + '" src="' + path_highlights_B08+''+i+extencion+'"/>';
html += '<img class="highlights center"     style="visibility:' + none + ';" data-index="' + i + '"  id="highlights_B09_' + i + '" src="' + path_highlights_B09+''+i+extencion+'"/>';


        }
        $this.html(html);

        this.attachHandlers(objIndex);
    };

    var startY = 0,
        thisTotal = 0,
        $downElem = null,
        lastY = 0,
        lastX = 0,
        lastVal = 0,
        isMouseDown = false;
    ThreeSixty.prototype.attachHandlers = function(objIndex) {
        var that = this;
        var $this = data[objIndex].$el;

        // add draggable events
        if(options.draggable){
            // if touch events supported, use
            if(typeof document.ontouchstart !== 'undefined' &&
                typeof document.ontouchmove !== 'undefined' &&
                typeof document.ontouchend !== 'undefined' &&
                typeof document.ontouchcancel !== 'undefined'){
                var elem = $this.get()[0];
                elem.addEventListener('touchstart', that.onTouchStart ,{passive: true});
                elem.addEventListener('touchmove', that.onTouchMove,{passive: true});
                elem.addEventListener('touchend', that.onTouchEnd,{passive: true});
                elem.addEventListener('touchcancel', that.onTouchEnd,{passive: true});
            }
        }

        // mouse down
        $this.mousedown(function(e){
            e.preventDefault();
            thisTotal = $(this).data('count');
            $downElem = $(this);
            startY = e.screenY;
            lastVal = $downElem.data('lastVal') || 0;
            lastX = $downElem.data('lastX') || 0;
            lastY = $downElem.data('lastY') || 0;
            isMouseDown = true;
            $downElem.trigger('down');


        });

        // arrow keys
        if(options.useKeys === true){
            $(document).bind('keydown', that.onKeyDown);
        }
        // mouse up
        $(document, 'html', 'body').mouseup(that.onMouseUp);
        $(document).blur(that.onMouseUp);
        $('body').mousemove(function(e){
            that.onMove(e.screenX, e.screenY);
        });
    };

    ThreeSixty.prototype.onTouchStart = function(e) {
        var touch = e.touches[0];
        //e.preventDefault();
        $downElem = $(e.target).parent();
        thisTotal = $downElem.data('count');
        var startX = touch.pageX;
        var startY = touch.pageY;
        var lastVal = $downElem.data('lastVal') || 0;
        var lastX = $downElem.data('lastX') || 0;
        var lastY = $downElem.data('lastY') || 0;
         isMouseDown = true;
         $downElem.trigger('down');
    };

    ThreeSixty.prototype.onTouchMove = function(e) {
/*        e.preventDefault();*/
        var touch = e.touches[0];
        scope.onMove(touch.pageX, touch.pageY);

    };

    ThreeSixty.prototype.onTouchEnd = function(e) {

    };

    ThreeSixty.prototype.onMove = function(screenX, screenY){

canvas()

        if(isMouseDown){
            var x = screenX,
                y = screenY,
                val = 0;

            $downElem.trigger('move');


            if(options.dragDirection === 'vertical'){
                if(y > lastY){
                    val = lastVal + 1;
                }else{
                    val = lastVal - 1;
                }
            }else{
                if(x > lastX){
                    val = lastVal + 1;
                }else if(x === lastX){
                    return;
                }else{
                    val = lastVal - 1;
                }
            }

            lastVal = val;
            lastY = y;
            lastX = x;
            $downElem.data('lastY', lastY);
            $downElem.data('lastX', lastX);
            $downElem.data('lastVal', lastVal);
            if(val >= thisTotal) val = val % (thisTotal - 1);
            else if(val <= -thisTotal) val = val % (thisTotal - 1);
            if(val > 0) val = thisTotal - val;
            val = Math.abs(val);



            $downElem.find('.threesixty-frame').css({visibility: 'hidden'});
            $downElem.find('.threesixty-frame:eq(' + val + ')').css({display: 'block'}).css({visibility: 'visible'});
            $downElem.find('.masks').css({visibility: 'hidden'}).attr("id","false")  ;
            $downElem.find('.masks:eq(' + val + ')').css({display: 'block'}).css({visibility: 'visible'}).attr("id","true");
            $downElem.find('.highlights').css({display: 'none'}).css({visibility: 'hidden'});
            canvas();


        }
    };


/*window.onload = function(e) {
canvas(e);
};*/



function canvas(e) {

var img= document.getElementById('true');

img.addEventListener('mousemove', function (e) {


var ctx;
this.canvas = document.createElement('canvas');
this.canvas.width = this.width ;
this.canvas.height = this.height;
 ctx=this.canvas.getContext('2d');
 ctx.drawImage(this, 0, 0, this.width, this.height);
const pixel = ctx.getImageData(e.offsetX, e.offsetY, 1, 1).data;
  
detectar_color(ctx,e,img);

} ,{passive: true} );



}





function detectar_color(ctx,e,img) {
$(document).unbind("click");
    
////DETECTAR COLORES
//Covierto Color RGBA a Hexadecimal
const pixel = ctx.getImageData(e.offsetX, e.offsetY, 1, 1).data;


var r=pixel[0] ;
var g=pixel[1] ;
var b=pixel[2] ;

function componentToHex(c) {
    var hex = c.toString(16);
    return hex.length == 1 ? "0" + hex : hex;
}




function rgbToHex(r, g, b) {
    return "#" + componentToHex(r) + componentToHex(g) + componentToHex(b);
}



var hex =rgbToHex(r, g, b);

console.log(hex);



if (hex==="#746280") {
$(document).unbind("click");
///B-01
var id = img.alt; 
var url="highlights_B01_";
var highlights_B01 = document.getElementById(url+id);
document.getElementById("true").setAttribute('title', 'B-01'); 
highlights_B01.style.display = "block";
highlights_B01.style.visibility = "visible";

$(document).click(function(e){
e.preventDefault();
var loc = window.location;
var pathName = loc.pathname.substring(0, loc.pathname.lastIndexOf('/') + 1);
var route= loc.href.substring(0, loc.href.length - ((loc.pathname + loc.search + loc.hash).length - pathName.length));
var url =route+"menu.html"
var level1="img/rdc/plans/B01/"
var level2=0
var url =route+"menu.html?level1="+level1+"&level2= "+level2+" "  ;
var myWindow = window.open(url , "_top", "");
$(document).unbind("click");
    e.stopImmediatePropagation()
})

}
else
{
var id = img.alt; 
var url="highlights_B01_";
var highlights_B01= document.getElementById(url+id);
highlights_B01.style.visibility = "hidden";

}



if (hex==="#568187") {
$(document).unbind("click");
///B-02
var id = img.alt; 
var url="highlights_B02_";
var highlights_B02 = document.getElementById(url+id);
document.getElementById("true").setAttribute('title', 'B-02'); 
highlights_B02.style.display = "block";
highlights_B02.style.visibility = "visible";

$(document).click(function(e){
e.preventDefault();
var loc = window.location;
var pathName = loc.pathname.substring(0, loc.pathname.lastIndexOf('/') + 1);
var route= loc.href.substring(0, loc.href.length - ((loc.pathname + loc.search + loc.hash).length - pathName.length));
var url =route+"menu.html"
var level1="img/rdc/plans/B02/"
var level2=0
var url =route+"menu.html?level1="+level1+"&level2= "+level2+" "  ;
var myWindow = window.open(url , "_top", "");
$(document).unbind("click");
    e.stopImmediatePropagation()
})

}
else
{
var id = img.alt; 
var url="highlights_B02_";
var highlights_B02= document.getElementById(url+id);
highlights_B02.style.visibility = "hidden";

}



if (hex==="#bf83cb") {
$(document).unbind("click");
///B-03
var id = img.alt; 
var url="highlights_B03_";
var highlights_B03 = document.getElementById(url+id);
document.getElementById("true").setAttribute('title', 'B-03'); 
highlights_B03.style.display = "block";
highlights_B03.style.visibility = "visible";

$(document).click(function(e){
e.preventDefault();
var loc = window.location;
var pathName = loc.pathname.substring(0, loc.pathname.lastIndexOf('/') + 1);
var route= loc.href.substring(0, loc.href.length - ((loc.pathname + loc.search + loc.hash).length - pathName.length));
var url =route+"menu.html"
var level1="img/rdc/plans/B03/"
var level2=0
var url =route+"menu.html?level1="+level1+"&level2= "+level2+" "  ;
var myWindow = window.open(url , "_top", "");
$(document).unbind("click");
    e.stopImmediatePropagation()
})

}
else
{
var id = img.alt; 
var url="highlights_B03_";
var highlights_B03= document.getElementById(url+id);
highlights_B03.style.visibility = "hidden";

}


if (hex==="#4b677e") {
$(document).unbind("click");
///B-04
var id = img.alt; 
var url="highlights_B04_";
var highlights_B04 = document.getElementById(url+id);
document.getElementById("true").setAttribute('title', 'B-04'); 
highlights_B04.style.display = "block";
highlights_B04.style.visibility = "visible";

$(document).click(function(e){
e.preventDefault();
var loc = window.location;
var pathName = loc.pathname.substring(0, loc.pathname.lastIndexOf('/') + 1);
var route= loc.href.substring(0, loc.href.length - ((loc.pathname + loc.search + loc.hash).length - pathName.length));
var url =route+"menu.html"
var level1="img/rdc/plans/B04/"
var level2=0
var url =route+"menu.html?level1="+level1+"&level2= "+level2+" "  ;
var myWindow = window.open(url , "_top", "");
$(document).unbind("click");
    e.stopImmediatePropagation()
})

}
else
{
var id = img.alt; 
var url="highlights_B04_";
var highlights_B04= document.getElementById(url+id);
highlights_B04.style.visibility = "hidden";

}


if (hex==="#bf7e89") {
$(document).unbind("click");
///B-05
var id = img.alt; 
var url="highlights_B05_";
var highlights_B05 = document.getElementById(url+id);
document.getElementById("true").setAttribute('title', 'B-05'); 
highlights_B05.style.display = "block";
highlights_B05.style.visibility = "visible";

$(document).click(function(e){
e.preventDefault();
var loc = window.location;
var pathName = loc.pathname.substring(0, loc.pathname.lastIndexOf('/') + 1);
var route= loc.href.substring(0, loc.href.length - ((loc.pathname + loc.search + loc.hash).length - pathName.length));
var url =route+"menu.html"
var level1="img/rdc/plans/B05/"
var level2=0
var url =route+"menu.html?level1="+level1+"&level2= "+level2+" "  ;
var myWindow = window.open(url , "_top", "");
$(document).unbind("click");
    e.stopImmediatePropagation()
})

}
else
{
var id = img.alt; 
var url="highlights_B05_";
var highlights_B05= document.getElementById(url+id);
highlights_B05.style.visibility = "hidden";

}


if (hex==="#ebbd72" || hex==="#eabc72" ) {
$(document).unbind("click");
///B-06
var id = img.alt; 
var url="highlights_B06_";
var highlights_B06 = document.getElementById(url+id);
document.getElementById("true").setAttribute('title', 'B-06'); 
highlights_B06.style.display = "block";
highlights_B06.style.visibility = "visible";

$(document).click(function(e){
e.preventDefault();
var loc = window.location;
var pathName = loc.pathname.substring(0, loc.pathname.lastIndexOf('/') + 1);
var route= loc.href.substring(0, loc.href.length - ((loc.pathname + loc.search + loc.hash).length - pathName.length));
var url =route+"menu.html"
var level1="img/rdc/plans/B06/"
var level2=0
var url =route+"menu.html?level1="+level1+"&level2= "+level2+" "  ;
var myWindow = window.open(url , "_top", "");
$(document).unbind("click");
    e.stopImmediatePropagation()
})

}
else
{
var id = img.alt; 
var url="highlights_B06_";
var highlights_B06= document.getElementById(url+id);
highlights_B06.style.visibility = "hidden";

}



if (hex==="#9ddbe2"  ||   hex==="#9ddae2"    ) {
$(document).unbind("click");
///B-07
var id = img.alt; 
var url="highlights_B07_";
var highlights_B06 = document.getElementById(url+id);
document.getElementById("true").setAttribute('title', 'B-07'); 
highlights_B06.style.display = "block";
highlights_B06.style.visibility = "visible";

$(document).click(function(e){
e.preventDefault();
var loc = window.location;
var pathName = loc.pathname.substring(0, loc.pathname.lastIndexOf('/') + 1);
var route= loc.href.substring(0, loc.href.length - ((loc.pathname + loc.search + loc.hash).length - pathName.length));
var url =route+"menu.html"
var level1="img/rdc/plans/B07/"
var level2=0
var url =route+"menu.html?level1="+level1+"&level2= "+level2+" "  ;
var myWindow = window.open(url , "_top", "");
$(document).unbind("click");
    e.stopImmediatePropagation()
})

}
else
{
var id = img.alt; 
var url="highlights_B07_";
var highlights_B07= document.getElementById(url+id);
highlights_B07.style.visibility = "hidden";

}

if (hex==="#9fbdc1" ||  hex==="#9fbdc0"    ) {
$(document).unbind("click");
///B-08
var id = img.alt; 
var url="highlights_B08_";
var highlights_B08 = document.getElementById(url+id);
document.getElementById("true").setAttribute('title', 'B-08'); 
highlights_B08.style.display = "block";
highlights_B08.style.visibility = "visible";

$(document).click(function(e){
e.preventDefault();
var loc = window.location;
var pathName = loc.pathname.substring(0, loc.pathname.lastIndexOf('/') + 1);
var route= loc.href.substring(0, loc.href.length - ((loc.pathname + loc.search + loc.hash).length - pathName.length));
var url =route+"menu.html"
var level1="img/rdc/plans/B08/"
var level2=0
var url =route+"menu.html?level1="+level1+"&level2= "+level2+" "  ;
var myWindow = window.open(url , "_top", "");
$(document).unbind("click");
    e.stopImmediatePropagation()
})

}
else
{
var id = img.alt; 
var url="highlights_B08_";
var highlights_B08= document.getElementById(url+id);
highlights_B08.style.visibility = "hidden";

}



if (hex==="#ec9b7b"  ||  hex==="#eb9b7b"     ) {
$(document).unbind("click");
///B-09
var id = img.alt; 
var url="highlights_B09_";
var highlights_B09 = document.getElementById(url+id);
document.getElementById("true").setAttribute('title', 'B-09'); 
highlights_B09.style.display = "block";
highlights_B09.style.visibility = "visible";

$(document).click(function(e){
e.preventDefault();
var loc = window.location;
var pathName = loc.pathname.substring(0, loc.pathname.lastIndexOf('/') + 1);
var route= loc.href.substring(0, loc.href.length - ((loc.pathname + loc.search + loc.hash).length - pathName.length));
var url =route+"menu.html"
var level1="img/rdc/plans/B09/"
var level2=0
var url =route+"menu.html?level1="+level1+"&level2= "+level2+" "  ;
var myWindow = window.open(url , "_top", "");
$(document).unbind("click");
    e.stopImmediatePropagation()
})

}
else
{
var id = img.alt; 
var url="highlights_B09_";
var highlights_B09= document.getElementById(url+id);
highlights_B09.style.visibility = "hidden";

}



if (hex==="#000000") {

document.getElementById("true").setAttribute('title', ''); 

}




}

    ThreeSixty.prototype.onKeyDown = function(e) {
        switch(e.keyCode){
            case 37: // left
             $el.prevFrame();
             //$el.canvas();
                break;
            case 39: // right
                $el.nextFrame();
               // $el.canvas();
                break;
        }
    };

    ThreeSixty.prototype.onMouseUp = function(e) {
        isMouseDown = false;

       // $downElem.trigger('up');
        


    };

    /**
     * Disables text selection and dragging on IE8 and below.
     */
    var _disableTextSelectAndDragIE8 = function() {
      // Disable text selection.
      document.body.onselectstart = function() {
          return false;
      };

      // Disable dragging.
      document.body.ondragstart = function() {
          return false;
      };
    };


    /**
     * A really lightweight plugin wrapper around the constructor,
        preventing against multiple instantiations
     * @param  {Object} options
     * @return {jQuery Object}
     */
    $.fn[pluginName] = function ( options ) {
        return this.each(function () {
            if (!$.data(this, 'plugin_' + pluginName)) {
                $.data(this, 'plugin_' + pluginName,
                new ThreeSixty( this, options ));
            }
        });
    };

})( jQuery, window, document );









  });


$(document).ready(function(){

var $threeSixty = $('.threesixty');
$threeSixty.threeSixty({
dragDirection: 'horizontal',
useKeys: true,
draggable: true,
});







var interval;





$('#control-play').click(function(e){

var mode = e.target.attributes.value.nodeValue;




if (mode=="play") {
document.getElementById("control-play").className = "control play icon-pause";  
interval = setInterval(play, 200);
e.target.attributes.value.nodeValue= "stop";
console.log(mode);
}



if (mode=="stop") {

document.getElementById("control-play").className = "control play icon-play"; 
clearInterval(interval);

e.preventDefault();
e.target.attributes.value.nodeValue ="play";
console.log(mode);

}




function play() {

$threeSixty.nextFrame();
}




});





$('.next').click(function(){
$threeSixty.nextFrame();


});

$('.prev').click(function(){
$threeSixty.prevFrame();
});


$threeSixty.on('down', function(){
$('.ui, h1, h2, .label, .examples').stop().animate({opacity:0}, 300);
});



 $threeSixty.on('up', function(){
 $('.ui, h1, h2, .label, .examples').stop().animate({opacity:1}, 500);
});



$('#control-zoom-in').on('click', function(e) {
changeZoom(10, e);




 });
$('#control-zoom-out').on('click', function(e) {
  changeZoom(-10 , e);
 });



 function changeZoom(amount, e) {
if (currheight === 600  ) return false;
  else {


var currheight =  $('.renders').css("height");

var newheight =  parseInt(currheight)  + amount;

 $('.renders').css("height" , newheight );
 $('.renders').css("z-index" , "0" );
 $('.masks').css("height" , newheight );
 $('.highlights').css("height" , newheight);


  }
  }



});




}
,
  // define methods under the `methods` object
  methods: {
  llamada: function () {




console.log("se mueve")



    },
    tocando: function () {




console.log("se toca")



    }




  }

}















</script>
<style type="text/css">
  

    
</style>