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

    // Channel IDs and Titles
    var channelId1 = 'UCXy10-NEFGxQ3b4NVrzHw1Q';
    var channelTitle1 = 'Eric Rosen Chess'; // Add a title for channel 1
    var channelId2 = 'UCZ1xMgtkHA0fIVdABCrUIww';
    var channelTitle2 = 'Eric Rosen Extra'; // Add a title for channel 2

    // API Calls
    var url1 = `https://www.googleapis.com/youtube/v3/search?key=${apiKey}&channelId=${channelId1}&part=snippet,id&order=date&maxResults=10`;
    var url2 = `https://www.googleapis.com/youtube/v3/search?key=${apiKey}&channelId=${channelId2}&part=snippet,id&order=date&maxResults=10`;

    // Fetch channel 1 videos
    fetchVideos(url1, channelTitle1);
    // Fetch channel 2 videos
    fetchVideos(url2, channelTitle2);

    function fetchVideos(url, channelTitle) {
        fetch(url)
            .then(response => response.json())
            .then(data => {
                var videos = data.items;
                var output = `<h3>${channelTitle}</h3>`; // Channel title
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
                // Append videos to the container without overwriting previous content
                var container = document.getElementById('youtube-videos');
                container.innerHTML += output;
            })
            .catch(error => console.error('Error:', error));
    }
});
</script>
