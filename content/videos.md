---
slug: videos
title: EricRosen Videos
layout: "page"
---

<div id="youtube-videos">
    <!-- Videos will be loaded here -->
</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
    // No secret keys are available for sites published on Github Pages
    // API key has been scoped to only calls to YouTube Data API v3 from this site
    var apiKey = 'AIzaSyCYd_ovvYuCUH9pa0FFOG8yDumRLY4q4Q8';
    // https://www.youtube.com/@eric-rosen
    var channelId = 'UCXy10-NEFGxQ3b4NVrzHw1Q';
    // Limited to the ten most recent videos
    var url = `https://www.googleapis.com/youtube/v3/search?key=${apiKey}&channelId=${channelId}&part=snippet,id&order=date&maxResults=10`;

    fetch(url)
        .then(response => response.json())
        .then(data => {
            var videos = data.items;
            var output = '';
            videos.forEach(function(video) {
                // Ensure the item is a video
                if(video.id.kind === "youtube#video") {
                    var videoId = video.id.videoId;
                    var videoTitle = video.snippet.title;
                    output += `
                        <div class="video">
                            <h4>${videoTitle}</h4>
                            <iframe width="350" height="197" src="https://www.youtube.com/embed/${videoId}" frameborder="0" allowfullscreen></iframe>
                        </div>
                    `;
                }
            });
            document.getElementById('youtube-videos').innerHTML = output;
        })
        .catch(error => console.error('Error:', error));
});
</script>
