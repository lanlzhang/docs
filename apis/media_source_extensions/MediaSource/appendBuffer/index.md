{{Page_Title}}
{{Flags
|State=Ready to Use
|Editorial notes=
|Checked_Out=No
}}
{{Standardization_Status|W3C Candidate Recommendation}}
{{API_Name}}
{{Summary_Section|Appends the specified media segment to the SourceBuffer.}}
{{API_Object_Method
|Parameters={{Method Parameter
|Index=0
|Name=data
|Data type=VARIANT
|Description=Type: ArrayBuffer. The media segment to append
|Optional=No
}}
|Method_applies_to=apis/media_source_extensions/MediaSource
|Example_object_name=SourceBuffer
|Return_value_name=
|Javascript_data_type=void
|Return_value_description=This method does not return a value.
}}
{{Examples_Section
|Not_required=No
|Examples={{Single Example
|Language=JavaScript
|Description=This example uses XMLHttpRequest to get a segment of video (range) from a file (url) and appends it to the current sourceBuffer.
|Code=<syntaxhighlight>//  Load video's initialization segment 
function initVideo(range, url) {
  var xhr = new XMLHttpRequest();
  if (range || url) { // make sure we've got incoming params
    // Set the desired range of bytes we want from the mp4 video file
    xhr.open('GET', url);
    xhr.setRequestHeader("Range", "bytes=" + range);
    segCheck = (timeToDownload(range) * .8).toFixed(3); // use .8 as fudge factor
    xhr.send();
    xhr.responseType = 'arraybuffer';
    try {   xhr.addEventListener("readystatechange", function () {
         if (xhr.readyState == xhr.DONE) { // wait for video to load
          // Add response to buffer
          try {            videoSource.appendBuffer(new Uint8Array(xhr.response));
            // Wait for the update complete event before continuing            videoSource.addEventListener("update",updateFunct, false);
          } catch (e) {
            log('Exception while appending initialization content', e);
          }
        }
      }, false);
    } catch (e) {
      log(e);
    }
  } else {
    return // No value for range or url
  }
}
function updateFunct() {
  //  This is a one shot function, when init segment finishes loading, 
  //    update the buffer flag, call getStarted, and then remove this event.
  bufferUpdated = true;
  getStarted(file); // Get video playback started
  //  Now that video has started, remove the event listener
videoSource.removeEventListener("update", updateFunct);
}</syntaxhighlight>
|LiveURL=
}}
}}
{{Notes_Section
|Usage=
|Notes=
|Import_Notes=
}}
{{Related_Specifications_Section
|Specifications={{Related Specification
|Name=Media Source Extensions
|URL=http://www.w3.org/TR/media-source/
|Status=W3C Candidate Recommendation
|Relevant_changes=
}}
}}
{{See_Also_Section
|Topic_clusters=Multimedia
|Manual_links=
|External_links=
|Manual_sections=
}}
{{Topics|Media}}
{{External_Attribution
|Is_CC-BY-SA=No
|Sources=MSDN
|MDN_link=
|MSDN_link=
|HTML5Rocks_link=
}}
{{Compatibility_Section
|Not_required=No
|Imported_tables=
|Desktop_rows=
|Mobile_rows=
|Notes_rows=
}}