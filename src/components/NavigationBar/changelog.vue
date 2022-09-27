<template>
        <b-nav-item @click="changelog">Changelog</b-nav-item>
</template>



<script>
import Swal from "sweetalert2";

/* eslint-disable */
function convertBlocklyHTMLElementToDisplayableContent(path, width, height) {
    let newPath = path
    newPath = path.replace(/transform="translate\([0-9\.\-]*,[0-9\.\-]*\)">/mi, `transform="translate(0,0)">`)
    let returned = `<svg xmlns="http://www.w3.org/2000/svg" xmlns:html="http://www.w3.org/1999/xhtml" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" class="blocklySvg" tabindex="0" width="${width}px" height="${height}px" style="display: inline;position: inherit;fill: white;font: bold 11px Helvetica Neue, Segoe UI, Helvetica, sans-serif">` + newPath
    returned += "</svg>"
    return returned
}
  var htmltext;
fetch('https://s4d-py.vercel.app/changelog.html')
    .then(function(response) {
        return response.text()
    })
    .then(function(html) {
        htmltext = html
    })
    .catch(function(err) {  
        console.log('Failed to fetch page: ', err);  
    });
export default {
    name: "Changelog",
    methods: {
        changelog() {
            Swal.fire({
                position: 'center',
                width: "900px",
                html: htmltext,
                confirmButtonText:
                '<i class="fa fa-thumbs-up"></i> Great!',
                confirmButtonAriaLabel: 'Thumbs up, great!',
            })
        },
    }
}
</script>
