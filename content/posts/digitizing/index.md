---
title: My Eight Year Quest to Digitize 45 Video Tapes
date: 2020-04-29
tags:
- mediagoblin
- clipbucket
- docker
- gcsfuse
---

I've carried this box of video tapes around for the last eight years. They've moved with me through four different apartments and one house. They're my family's home videos from my childhood.

TODO: Picture of tapes

After eight years and 600 hours of work, I finally digitized and organized them well enough to throw away the original tapes. Here's what they look like now:

TODO: Screenshot of sharing site

There are . It's 513 separate clips. Each clip shows the title, a description, the recording date, which tape it came from, who's in it, a description of what's going on, and how old everyone is at the time of the recording.

{{< img src="mediagoblin-single-video.jpg" alt="Screenshot of MediaGoblin displaying a video" caption="Viewing a video on MediaGoblin" maxWidth="600px" >}}

This post explains how I did it and why it took me eight years.

## That doesn't sound so hard

If you're wondering why it took so long, I don't blame you. I thought it would be an easy project too.

These are family artifacts, and I'm not willing to throw away the tapes until I'm confident that I've captured all of the data accurately. But once you start doing it, you realize that capturing the data accurately isn't as simple as it seems. There's metadata on the tapes. Some of the tapes have labels that give clues about the recording dates. There's ordering to the clips that's also important for establishing dates. If someone says the date in clip A then the date in clip C, you know that clip B must be between dates A and C. But if you naively approach it the way I originally did, just saving the clip as "Michael plays with water balloons.mp4" then you lose that metadata.

## My naive first try

Around 2010, my mom bought some sort of VHS to DVD converter and ran all of our home videos through it.

{{< img src="original-dvds.jpg" alt="Photo of rewritable DVDs labeled by letter" caption="The original DVD copies of the tapes my mom made. I'm not sure what happened to the missing letters." maxWidth="600px" >}}

The problem was that there was only one set of DVDs. At that point, everyone in my family lived in a different state, so it wasn't like we could easily trade the DVDs back and forth. So in 2011, I got the DVDs from my sister, converted the DVDs to AVI files and threw them all up on cloud storage. Problem solved! Now everyone can access them!

TODO: Screenshot of files on GCS

A few weeks later, I asked people if they'd watched any of the tapes, and nobody had. I hadn't either. In the age of YouTube, it seemed so boring to download a 3-hour mystery clip and then jump around in search of interesting footage.

The only person who was excited about it was my mom. "Okay, great," she said, "Now, can I finally throw out all these tapes?" That was a scary question. What if there were tapes that we missed? What if we could do better on quality?

I realized that I'd never feel comfortable throwing away the original tapes until I was confident that I captured everything we wanted from them. That meant capturing the footage itself at the highest quality.

## Digitization: from start to finish

TODO: Diagram of the whole process

In reality, my path was messier, because I'd reach stage three, realize I screwed up stage one, then have to start all over again. For the sake of everyone's sanity, I'm explaining the process stage by stage instead of forcing you, my beloved readers, to constantly jump backwards and restart along with me.

## Part 1: Digitizing

I told my mom I'd handle the original tapes, and so the next time I saw her, she handed me a huge cardboard box of the old tapes.

The obvious solution would be to outsource it to a professional. There are plenty of digitization services, including companies who specialize in processing old home videos.

I'm fairly privacy sensitive. I'm not going to hand over footage of me potty training (at the appropriate age, nothing weird!) to a random company for whom security is an afterthought. Besides, I thought, how hard could it be to digitize video?

Spoiler alert: really hard.

For my first attempt, I asked my dad to give me the old family VCR that was still in his basement. I bought a cheap RCA to USB adaptor from Amazon, and I was off to the races. To capture the raw video, I used VirtualDub, which was kind of dated at the time, but for 2012, not *that* dated.

TODO: VCR picture

To cut the videos into clips, I used Adobe Premiere Elements, a product I still happily use today. As I started the editing process, I realized that the audio and video was slightly out of sync. Okay, no problem. I can just shift the audio a little bit. But ten minutes later, I'd realize that it was out of sync. The skew would get progressively worse the deeper I got into each tape.

I spent hours stubbornly and meticulously shifting audio. Do you know how hard it is to fix a clip's audio when you can't tell if a sound is happening 10 milliseconds too early or 10 milliseconds too late? It's really hard! Judge for yourself. Here's a video of me playing with my poor, patient kitten Buddy. The audio is slightly out of sync with the video, but is the audio ahead of the video or behind?

{{< video src="buddyjump.mp4" caption="Second implementation: extra \"lock\" controls are ugly and confusing" >}}

Here's the part where Buddy jumps, slowed down to 1/5th speed:

{{< video src="buddyjump-slowmo.mp4" caption="Second implementation: extra \"lock\" controls are ugly and confusing" >}}

Answer: The audio is coming in a few milliseconds late.

### Maybe I should spend an extra hundred dollars instead of wasting hundreds of hours

After an embarrassing number of hours, I realized that all this time was probably because I skimped on the video capture device. I had just purchased the cheapest one I saw on Amazon, but maybe a better one would capture without the headache.

So, I bought another one! And then after hours of capturing footage from that, I realized I still had the same problem. After a bit of research, it seemed that the problem was with the VCR itself. So, I researched high-end VCRs. Nobody makes them anymore, but you can find good ones on eBay. I spent $XX on a XXX because it had S-Video output. I don't really know what difference that made, but it seemed like it was better than RCA, so I was excited. I bought a *third* video capture card and tried hooking it up.

{{< img src="jvc-vcr.jpg" alt="Photo of expensive VCR with S-VHS support" caption="The mint condition JVC SR-V10U VHS ET Super VHS Professional Series VCR that I bought on eBay for $XX." maxWidth="600px" >}}

As luck would have it, it didn't work. At this point, I had three different video capture cards, two different VCRs. Women I dated at the time would come to my apartment and think that I was some sort of antique video equipment hoarding nutjob.

{{< img src="s-video-capture.jpg" alt="TODO" caption="TODO" maxWidth="300px" >}}

### Surrendering to digitization professionals

Fast forward to 2018. I had dragged these videotapes to two different apartments, and I was preparing to move from New York City to Massachusetts. I couldn't justify dragging all the VCRs and video equipment too when it had become clear that I wasn't going to ever finish the project on my own.

At this point, years had passed. I had invested hundreds of hours into experimenting with different settings. There were long gaps because it was a pain to drag out the VCR, hook it all up, and fiddle with sketchy Chinese device drivers. The cost of getting everything out and put away was about 30-40 minutes, so it only made sense on the weekends, when I had long blocks of free time to get into it. But the project often frustrated me, so I never wanted to do it on the weekend unless I was really bored or anxious to get rid of the tapes.

I reconsidered using a digitization company. I still didn't like the idea of handing over my family's most intimate memories to strangers, but I felt like they'd be able to capture the footage at a higher quality than I could ever achieve by myself.

And they did. The quality was .

TODO: Show side by side of video quality

{{<notice type="info">}}
**A brief rant about EverPresent**

To capture the footage, I worked with a company called EverPresent, and I found their data security and customer service practices to be severely lacking.

All EverPresent packages require the customer to receive their files via cloud storage, so I declined their add-on option for storing a copy on an USB hard drive. Despite this, they gave me an external hard drive with a copy of my files and wanted to charge me several hundred dollars for it. They took back the hard drive, but I have to take it on faith that they securely wiped my files before providing the same device to another customer. They also billed me a higher fee than we had agreed and only relented after I forwarded them an email where their rep quoted me the lower price.

When I looked at the instructions for accessing my files on cloud storage, I realized they had a huge security hole. that the password was just duplicated from the URL. They published all their customers videos in a way that anyone could guess most of their customers' URLs. They were password protected, but the password matched the URL, so if you found a valid URL, you knew the password.

I reported the issue to them, and, to their credit, they quickly and professionally escalated it to their CEO and head of XX. They promised to remediate the issue within weeks, but then nothing happened. I contacted them a couple months later to check on status, and they said that they decided against fixing the issue, but switched to a new password scheme. They said that they could tell from their Box.com logs that nobody was exploiting this issue in the wild (sidenote: I'm not sure that Box.com offers logging to verify this), so they just let existing customer URLs expire after six months and switched future customers to the more secure password scheme. They never shared details of their new password scheme with me except to say XXX.
{{</notice>}}

## Part 2: Editing

My experience with home videos is that 90% of the footage is boring, 8% is entertaining, and 2% is amazing. That means that after you digitize the tapes, there's still lots of work to do.

### Critical for editing: a zoomable timeline

Editing a home video really comes down to finding the boundaries between different clips. VHS tapes contain a long stream of different video clips and dead air, so you have to find where each clip starts and ends.

I tried a few different tools, but nothing came close to Adobe Premiere Elements. It's still available without a monthly subscription for under $100. Its killer feature is the the zoomable timeline.

When editing, I generally wanted to zoom out to find the rough boundary between clips and then zoom in so I could move frame-by-frame to find the exact ending spot.

TODO: Screenshot of Premiere

### The downsides of Adobe Premiere

The biggest problem with Premiere is that it requires a lot of starting and stopping. My process was:

1. Open a raw capture file containing 30-120 minutes of video.
1. Mark the boundaries of an individual clip.
1. Export the clip.
1. Wait 2-15 minutes for exporting to complete.
1. Go back to (2) until the tape is complete.

The long waits meant that I could only do this work if I was constantly context-switching between video editing and some other task.

But in my first attempt, I just sucked it up and spent hours doing it this inefficient way. When I reached the point of sharing the clips online, I realized I'd made a grievous error. When I exported each clip, I just gave each one a title like `Michael dancing to the radio.mp4`. But there was a lot more metadata that I wanted to display

1. What's happening in this clip?
1. Which people and pets appear in this clip?
1. When was this video recorded?
1. Which tape did it come from?
1. Where on the tape did it appear?

(4) and (5) are not that interesting in themselves, but I could use those details to estimate the recording date when there were no other clues.

One of the other fatal flaws of this workflow is that it's not easily reproducible. Fixing a small error is about as hard as doing the entire thing from scratch. For example, when I reached the sharing stage, I realized that I should have exported the video in a format that browsers can play natively. Because I didn't do that, I either had to re-do the tedious process of exporting hundreds of clips by hand or I had to degrade quality by transcoding the already-exported video to a different format.

### Robo-editing

After an embarrassing number of hours doing everything by hand, I wondered if it was possible to automate this process. The advantage of dragging my feet so long on this project was that machine learning had time to catch up with me. Throughout the 2010s, machine learning was getting better and cheaper. I knew that no automated solution would get it perfect, but maybe it could do 80% of the work and I could fix the last 20% by hand.

I experimented with a tool called [pyscenedetect](https://pyscenedetect.readthedocs.io/en/latest/). It uses machine learning to detect scene changes and prints out the timecodes where the scene changes happen:

```bash
 $ docker run \
    --volume "/videos:/opt" \
    handflucht/pyscenedetect \
    --input /opt/test.mp4 \
    --output /opt \
    detect-content --threshold 80 \
    list-scenes
[PySceneDetect] Output directory set:
  /opt
[PySceneDetect] Loaded 1 video, framerate: 29.97 FPS, resolution: 720 x 480
[PySceneDetect] Downscale factor set to 3, effective resolution: 240 x 160
[PySceneDetect] Scene list CSV file name format:
  $VIDEO_NAME-Scenes.csv
[PySceneDetect] Detecting scenes...
[PySceneDetect] Processed 55135 frames in 117.6 seconds (average 468.96 FPS).
[PySceneDetect] Detected 33 scenes, average shot length 55.7 seconds.
[PySceneDetect] Writing scene list to CSV file:
  /opt/test-Scenes.csv
[PySceneDetect] Scene List:
-----------------------------------------------------------------------
 | Scene # | Start Frame |  Start Time  |  End Frame  |   End Time   |
-----------------------------------------------------------------------
 |      1  |           0 | 00:00:00.000 |        1011 | 00:00:33.734 |
 |      2  |        1011 | 00:00:33.734 |        1292 | 00:00:43.110 |
 |      3  |        1292 | 00:00:43.110 |        1878 | 00:01:02.663 |
 |      4  |        1878 | 00:01:02.663 |        2027 | 00:01:07.634 |
 ...
```

It did indeed get about 80% of it right, but the work I had to do to verify correctness cost more than the time I saved from automating it.

Nevertheless, pyscenedetect did spark one of my most important realizations of this entire project: CSVs can represent rich clip metadata.

### I remembered that I'm a programmer

Up until this point, I'd been treating the video files as these impenetrable blobs that I couldn't interact with except with pre-made tools. pyscenedetect outputs a CSV file so that you can consume the metadata with other tools. 

I realized that videos are, in fact, not a dark and mysterious blobs of data that I need to edit via interactive tools. There are plenty of libraries and command-line tools that automate video editing. Instead of chopping up clips in a tool like Premiere, I could just record the start and end times of each clip and use whatever tool I wanted to cut the clips at those positions.

I ended up with a spreadsheet that looked like this:

TODO: Screnshot of spreadsheet

I then wrote a script that took that CSV and a list of raw video files and chopped them up into smaller clips. The tool that does the heavy lifting is ffmpeg, one of the most popular open source tools for working with video.

### The surprising challenge of finding frame numbers

One tricky part of this is that ffmpeg edits in terms of frame numbers. I couldn't figure out a way to get Premiere to display the current frame number. VLC Media Player didn't seem to offer this either. After researching, it turned out the only popular player that offers this as a native feature is QuickTime player. I tried for a while to use QuickTime to find the clip boundaries, but to do this well, you really need Premiere's zooming in and out feature and the ability to step back frame by frame or jump a few frames at a time.

I found instructions for using ffmpeg to *add* frame numbers to all of my videos. So I just made a scratch copy of all the videos with a superimposed frame number. That allowed me to use Premiere to find the frame boundaries and just record the data in my spreadsheet.

You'll notice that there are many more columns in the spreadsheet than the frame boundaries. I'll explain those when I get to the section describing how I shared these clips.

### The glory of an automated solution

At this point, I had literally spent **hundreds** of hours going through the tedious process of selecting clip boundaries in Premiere, hitting export, waiting a few minutes for it to complete, then starting over. And because I had to repeat this process so many times either because I didn't capture the raw footage well enough or I didn't preserve all the metadata I wanted, I had repeated this whole process 2-3 times for each clip.

Once I had it scripted, it was a huge weight off my shoulders. I didn't have to worry that I was dropping metadata or I picked the wrong format. If there was anything I missed, I could just tweak my script, run it again, and it would all be fine.

## Part 3: Sharing

I had a bunch of clips now, and I wanted a way to share them. From my naive first approach, I knew that nobody would want to just download a bunch of opaque files from cloud storage.

My first attempt at sharing these clips was in 2016, so YouTube, Vimeo, and Netflix were firmly established. Everyone had come to expect that they should be able to watch videos by searching a web interface that showed thumbnails and metadata about each clip.

I wanted to create a private YouTube that only my family could access.

### ClipBucket, the cheap YouTube clone

ClipBucket seemed to fit the bill. It was an open source YouTube clone. Puzzlingly, they didn't seem to offer installation instructions, but I found a random guide that showed me how to install it on Ubuntu. I converted that guide into an Ansible playbook (TODO: link) to automate the process, so I could spin up a ClipBucket instance on a local VM or on a Google Compute Engine cloud VM. ClipBucket was [very excited to see a Google employee](https://clipbucket.com/2016/09/17/clipbucket-into-googles-doors/) using ClipBucket, even though I was always careful not to interact with them in my capacity as a Google employee.

It was a little tricky to figure out how to serve the videos. I had XX GB of videos, and I didn't want to have to re-upload everything if I ever had to wipe the VM. Disk space for local VMs is also relatively expensive, so I didn't want to pay for a huge disk either.

I found gcsfuse, an open source library that allows you to mount Google Cloud Storage buckets as a Linux directory. So, I did that.

That worked fine, but I ran into issues installing ClipBucket's updates. The first time I wrote my automation, I found bugs that prevented me from initializing ClipBucket's database. They seemed like strange oversights. Their built-in script contained duplicate primary keys, which MySQL would reject. My solution just used find and replace to eliminate the redundancy, but I figured that ClipBucket must have some internal script that avoids this, so they would promptly fix it after I reported it. To make matters more interesting, I was employed by Google at the time, and I wasn't allowed to contribute to open source projects without explicit permission, so I couldn't fix it myself, but I was allowed to write highly pointed bug reports.

They never fixed those bugs. Slowly, I started to realize that maybe the company that makes its money by charging customers to install its software isn't that interested in making their software easy to install.

### MediaGoblin, a more modern alternative

After using ClipBucket for initial versions, I reassessed what was available. I found MediaGoblin. Unlike ClipBucket, it had an official Docker image. What could be easier to install than that? And it was Python-based, as opposed to ClipBucket, which was the less elegant PHP.

Even better was that it was very developer friendly. It offered a simple CLI for importing videos and supplying metadata.

It's a GNU project, which is a little bit frustrating. They only use infrastructure that's also GPL, so they refuse to touch Github or Gitlab. Contributing to their codebase requires you to:

1. Apply for an account on [their Trac server](https://issues.mediagoblin.org/)
1. File a bug report
1. Supply a URL to your patch
1. Wait for them merge in your patch via command-line tools and publish the result to their [git repository](https://savannah.gnu.org/projects/mediagoblin).

It felt like contributing to an open source project in 2005. I submitted [a](https://issues.mediagoblin.org/ticket/5574) [few](https://issues.mediagoblin.org/ticket/5575) [patches](https://issues.mediagoblin.org/ticket/5576), but even filing the bugs took months because their Trac server was [blocking registrations](https://imgur.com/NOjfHI7). When they finally allowed me to register, it would still be 11 months before they responsed to any of the patches I submitted.

### Re-dockerizing MediaGoblin

The [MediaGoblin wiki](https://wiki.mediagoblin.org/EasyDeployment) pointed to a [Docker image](https://notabug.org/dachary/mediagoblin-docker). I was able to run the pre-built Docker image successfully. But I soon realized I needed a couple changes to the 

By default, MediaGoblin will attempt to re-transcode every video you give it. You can [adjust the configuration](https://wiki.mediagoblin.org/Configure_MediaGoblin#Disable_transcoding) to skip transcoding for videos that are already web-ready, but the pre-built Docker image didn't support that.

I also needed to enable authentication. If I was going to put this on the public Internet, I needed a way to prevent anyone who stumbles upon the server from accessing all the files. MediaGoblin does have an authentication plugin, but who knows whether it even works or provides any real protection. Instead, I decided to use nginx's HTTP Basic Authentication feature, as it's pretty well battle tested.

I spent so much time tinkering with the MediaGoblin docker image that it probably would have been faster for me to just write my own simple video-sharing web app from scratch.

I tried forking the repo and building my own copy, but it didn't work. After lots of poking around and Googling error messages, I finally got it to work. But then six months later, the image stopped building again. A bunch of MediaGoblin's dependencies had changed drastically due to the Python 2 end of life, so now everything was broken. Fortunately, I saw that one of MediaGoblin's maintainers had made their own Docker image for Python3, so I incorporated that into my image and was up and running again. Then, when I was writing this blog post, I realized the image was broken again. This time, I abandoned my commitment to base the Docker image on the mainline MediaGoblin docker image and just pointed it at my own fork instead and tagged a release where all of the dependencies are exact matches for a specific version rather than >= to some version.

But I finally got it working.

### If I were to do this again

MediaGoblin is alright now that I've got a working image, but MediaGoblin's dependencies are pretty coarsely defined, so I have to fix . The project seems to be mostly dead, though some contributors held a meeting a few months ago to discuss jumpstarting development again. For simple video sharing, it's too much complexity.

If I were doing this again, I'd use a static site generator like Hugo or Jekyll. I originally chose tools like ClipBucket and MediaGoblin to avoid the problem of transcoding video and playing it in the browser, but I've since realized that those problems are easy to solve. Modern browsers natively support video, and a variety of tools to encode video to a browser-compatible format.

One downside of using a static site generator is that you lose the ability to dynamically add comments. Everything is much simpler if all of the data is read-only as opposed to having to maintain dynamic state on the server. You could use Commento or Disqus if you wanted to. Even when I used platforms that supported it, my family never used the in-app commenting feature and instead just commented on videos over group texts.

The other thing you lose from a static site is the ability to search.

## Part 4: Hosting

When I first started launched a sharing solution, I just used a regular Google Compute Enginge VM and ran my Ansible playbook to install ClipBucket. That was a pain, though, because I had to maintain an entire server VM, when all I cared about was the one video-sharing app.

By the time I switched to MediaGoblin as my hosting software, I'd seen how much better it was to host with Docker, so I did that.

When I graduated to Docker, I continued using GCE, but I just kept a VM running all the time.

### MediaGoblin and the video storage problem

I again ran into the problem of how to share XX GB of video. I could theoretically stuff them all into the Docker image, but that felt ugly and expensive. I figured that I could follow the same process as I did with ClipBucket - put the videos on GCS, then symlink all of MediaGoblin's folders to GCS folders via gcsfuse. It turns out that mounting a GCS bucket into a Docker container is much harder than mounting it in a normal VM. I spent dozens of hours solving all the gotchas and wrote a [whole blog post](/retrofit-docker-gcs/) about it.

{{< img src="mg-gcs-architecture.jpg" alt="Architecture diagram of MediaGoblin + Docker + gcsfuse" caption="Architecture for deploying MediaGoblin to Google Cloud Platform from my [2018 post](/retrofit-docker-gcs/)" maxWidth="600px" hasBorder="True" >}}

Crushingly, after all the hours getting it to work, I realized it was unusably slow. It took about 20 seconds just to load all the video thumbnails on the homepage. I tried switching to a more powerful VM, but I still got the same result.

The bottleneck was in reading and writing of the video files and thumbnail images. To serve any data, my MediaGoblin had to read it from Google Cloud Storage via gcsfuse, probably not optimized for speed. Then it had to send the same data to the browser. But MediaGoblin was a pointless middleman. For the static files, it was just a dumb proxy.

It would be better if the browser could just bypass MediaGoblin entirely for static files and grab them directly from GCS.

TODO: Diagram of interaction between browser and GCS.

{{<notice type="danger">}}
**Note**: There's a security vulnerability here because it means that any user who knows the proper URL can access all of my files without authentication. I'm relying on the difficulty of guessing my filenames.
{{</notice>}}

The downside is that all the work I did to make gcsfuse work under Docker was actually completely unnecessary.

### Running 24/7 to satisfy 2 hours of demand per year

I ran MediaGoblin in a dedicated Docker image for about a year before it occurred to me how wasteful this was. It's nice for my family's MediaGoblin instance to be available whenever we're in a nostalgic mood to watch old home videos, but it's not the kind of thing you visit every day. I'd estimate that the server gets about 10 hours of usage collectively per year, but I was running it nonstop.

When Google introduced Cloud Run, a service to launch Docker instances on-demand, I thought that would be a cool solution. I'd leave the Docker instance off and then anytime someone made an HTTP request, Google would spin up my MediaGoblin instance and run until it expires. I'd only pay for the time the server actually ran, which was basically nothing.

I ended up having trouble getting it to run on Google Cloud Platform. I can't recall the details now, but Google seems to do something unexpected when your Docker container needs to do things as the `root` user. I ended up deploying with Heroku instead, and everything was smooth sailing.

TODO: Explain how to set up the Heroku part and point it to the repo.

```bash
heroku login -i
heroku container:login

HEROKU_APP_NAME="your-heroku-app-name"
HTTP_AUTH_USER="some-username-to-access-your-mediagoblin-instance"
HTTP_AUTH_PASS="some-password-to-access-your-mediagoblin-instance"
GCS_BUCKET="your-gcs-bucket"
MEDIAGOBLIN_DB_URL="public-URL-of-your-mediagoblin.db-file"
HTML_TITLE="My MediaGoblin Instance"

heroku container:push web \
    --app "$HEROKU_APP_NAME" \
    --arg "HTTP_AUTH_USER=${HTTP_AUTH_USER},HTTP_AUTH_PASS=${HTTP_AUTH_PASS},GCS_BUCKET=${GCS_BUCKET},MEDIAGOBLIN_DB_URL=${MEDIAGOBLIN_DB_URL},HTML_TITLE=${HTML_TITLE}"

heroku container:release --app "$HEROKU_APP_NAME" web
```

## The final workflow

TODO: Show a walkthrough using the demo footage.

1. Digitize video tapes into high quality raw footage.
1. Use ffmpeg to copy each raw video with frame numbers overlaid on the screen.
1. Create a spreadsheet to track start and end frame numbers for each scene and any metadata you want to capture.
1. Use Adobe Premiere Elements to view each clip and populate the spreadsheet.
1. Run [`csv_to_yaml`](https://github.com/mtlynch/process-home-videos) to convert the CSV to a YAML file.
1. Run [`render_scenes`](https://github.com/mtlynch/process-home-videos) to chop the raw footage into individual scenes.
1. Run [`publish_to_mediagoblin`](https://github.com/mtlynch/process-home-videos) to create a mediagoblin database file
1. Move the MediaGoblin database file and all the processed scenes to Google Cloud Storage.
1. Deploy a custom MediaGoblin Docker image to Heroku.

## Tips for anyone about to try this

* Capture as much metadata as possible during the entire capture process.
  * Labels on the tapes might turn out to be handy.
  * Keep a record of which clip came from which tape and in what order.
  * Make note of any clues about the recording date in the clip.
* Consider outsourcing the raw capture to professionals.
  * It will be *really* difficult and expensive for you to achieve the same quality capture as a company that does dedicated video digitization
  * That said, I don't recommend EverPresent.
* Capture as much of the data in an application-agnostic format
  * Clip descriptions, time codes, dates, etc.
  * If you keep it in an application specific format (or worse, throw it away), it's difficult for you to reproduce the work if you decide on a different solution.
  * When you watch the videos during editing, you're seeing lots of useful metadata. You'll lose it if you don't capture it.
    * What's happening in the video?
    * Who's in the video?
    * When was it recorded?
    * Is this video good? I tag my favorite clips "best of"
* Build the end-to-end solution as soon as possible.
  * I wish I had started with a single tape and then did the work necessary to share that rather than digitize, edit, and share, then have to keep jumping back to earlier stages when I found mistakes later on.
* Make a montage!
  * Slow show is great. I discovered this by mistake.
  * Montages are all about the music. "Slow Show" by The National is amazing for montages and nobody knows.

## Doing this yourself

I didn't generalize it too much, because I imagine that everyone will have their own preferences for exactly how to digitize their data, but you can see an end-to-end example of how I digitized a tape of found footage in the public domain using the same method as I digitized my home videos.

## Source code

| Repository  | Description |
|-------------|-------------|
| [MediaGoblin](https://github.com/mtlynch/mediagoblin) | Mirror of the MediaGoblin core repo + Circle CI configuration.<br><br>The branch [mtlynch-custom](https://github.com/mtlynch/mediagoblin/tree/mtlynch-custom) has custom fixes for my instance (replaces their old video player and trims some parts of their UI that I don't need). |
| [mediagoblin-docker](https://github.com/mtlynch/mediagoblin-docker) | Builds a Docker image for MediaGoblin. The Docker image includes support for [nginx](https://nginx.org/en/) and an option to enable [HTTP Basic Authentication](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#Basic_authentication_scheme). |
| [process-home-videos](https://github.com/mtlynch/process-home-videos) | Python scripts for chopping up raw video files into clips and then publishing those clips to MediaGoblin. |

---

*Cover art by [Loraine Yow](https://www.linkedin.com/in/lolo-ology/).*