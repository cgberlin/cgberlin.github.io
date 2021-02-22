## Professional Self-Assessment

The past handful of years working on this coursework (not all in the ePortfolio, but my academic studies as a whole) have been an amazing ride. I am fortunate enough to have discovered my passion at a young age, and even more fortunate in that I was able to develop a career in my chosen field while studying at the same time. Having the opportunity to see the direct, real-world applications and utilization of the theory I was learning in school was invaluable in developing my understanding of Computer Science. There were many times where I was learning how a specific algorithm, database, or architecture was implemented at a very low-level in school while using it wrapped by some package or high-level application at work. I believe that a lot of my strength as a programmer can be directly attributed to that dual/tandem learning. 

Like many other developers and engineers that I know my side-projects rarely (except on rare, special occasions) get "finalized" without some type of outside prompt. I wanted to use this ePortfolio as an opportunity to wrap up one or two of those side-projects that I felt provided some type of real, tangible value, and I am happy to say that I feel successful in that goal. My father's new photography website [Bright Blue Waves](https://brightbluewaves.com) is completely serverless and scalable, easy to maintain, he can manage the content seemlessly, and I got to play with a bunch of new frameworks that looked interesting ([Forestry](https://forestry.io/)). The other artifact used, my [AWS FFMPEG wrapper](https://github.com/cgberlin/aws-ffmpeg-lambda) has already seen real-world use, and I am glad to have a cleaned-up example to reference. 


### Artifacts Used

[Bright Blue Waves](https://github.com/cgberlin/brightbluewaves)

brightbluewaves.com is a serverless content-management system and front-end for my father's photography. 
Built using a combination of Forestry, Gridsome, Vue.js, and deployed on netlify for a full "cloud" experience. 

![bright blue waves landing page](https://lucianet.s3.amazonaws.com/Screenshot_20.png)

[AWS FFMPEG Lambda](https://github.com/cgberlin/aws-ffmpeg-lambda)

This lambda function wraps ffmpeg to allow for easy, cheap, and fast transcoding of videos. The current function deployed is triggered on S3 bucket upload; it watches for videos to transcode to frames which are then saved to another S3 bucket. 

![aws lambda pipe](https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-RealTimeFileProcessing.a59577de4b6471674a540b878b0b684e0249a18c.png)


### Informal Code Review

I recorded a quick walkthrough of the two projects/artifacts with some proposed changes and updates.
[Code Review on Streamable](https://streamable.com/9pyzvg)


### Enhancements, Updates, and Narratives

#### Software Design and Engineering

The artifact I chose for this milestone is the Vue.js front-end and flat-file content management system associated with [brightbluewaves.com](https://brightbluewaves.com). This artifact is open-source with the code residing [here](https://github.com/cgberlin/brightbluewaves). Because the project is open source in nature, we can see that I originally forked the project twenty-six days ago when I had the idea to make a photography site for my father. Since this artifact is forked from another open-source repository it has taken a fair amount of work to bend it to my specific needs. I also used this project as an opportunity to teach someone near me a little bit about Vue front-end development and flat-file content management systems. As a result, the codebase was left almost completely undocumented and in the perfect state for an update/final polish. I also like that the project has a real-world use case and is deployed.

I have met most of the objectives I set out to. Originally I planned on renaming some of the actual source classes and files from generic names like “Project” to something a little more specific, but opted against that in favor of modularity and expanding the existing project (there was more than enough work there). Comments and documentation have been added throughout the existing codebase (ex 1), and all user interface updates other than the contact form are complete. I added a new field to the “Projects” collection called “author” to further support modularity and the use case of my father allowing guest posts (ex 2). I made a new component called ProjectHeader to fix the display at the top of each post (ex 3), updated the scroll-to-top image and spacing, added proper copyright text, and fixed multiple CSS issues. 

The majority of the updates are in this [commit](https://github.com/cgberlin/brightbluewaves/commit/5cf3c8278d9b77ef9f581b3838a66e52513ec4bb).

ex. 2 

{% raw  %}
{%
<!-- conditionally show pipe + author if it exists -->
<h2 class="project-title">{{ title }} {{author ? `| ${author}` : ''}}</h2>
%}
{% endraw %}

ex. 2
```
author: {
  type: String,
  required: false
}	    
```

ex. 3
```
<!-- Displays the meta data for a project in a header/title form. Used for individual post. -->
<template>
  <section class="project-header">
    <div class="project-title-row">
      <h2 class="project-title project-title-text">{{ title }}</h2>
      <h2 class="project-title project-author-text">{{ author }}</h2>
    </div>
    <time class="project-year" :datetime="year">{{ year }}</time>
  </section>
</template>
```

#### Algorithms and Data Structures

The artifact I chose for this milestone is the [AWS Lambda function](https://github.com/cgberlin/aws-ffmpeg-lambda). This function watches an AWS S3 storage bucket for any file uploads, checks if it was an allowed video type, extracts each frame if it was, and then saves the resulting frames to a new S3 bucket. It was created originally six months ago out of a direct need for work and is still being used (in some form) at my company. The concept is deceptively simple, as getting ffmpeg to even run inside of a Lambda function was an incredibly difficult task. 

I chose this artifact for numerous reasons and am happy with both the overall presentation in relation to “Algorithms and Data Structures” and the improvements made. While I do think that using a compiled language for a program which utilizes a search tree or complicated sort might demonstrate algorithm-proficiency better, I didn’t have a pressing need for one. I wanted each artifact in this portfolio to have a use and purpose, as so many of my side projects and little libraries never get truly finished or polished. Numerous improvements were made as documented by this [commit](https://github.com/cgberlin/aws-ffmpeg-lambda/commit/417c7334af3c2b54711e8c1878a17283ff62f8e9). Since the repository is public it might be easier for you to see the diff there. In summation, the entire codebase was updated to ES6 (ex 1), syntax was fixed everywhere including standardization of variable naming, explanatory comments were added throughout the source code, a bug was fixed that caused the code to only function properly if the video was called ‘input.mp4’ (ex 2), and some hardcoded values were moved to environment variables (ex 3). 

ex. 1
```
ffmpeg.on('error', function (err) {	      ffmpeg.on('error', (err) => {
  console.log(err)	                         console.log(err);
  console.log('ffmpeg err')	                 console.log('ffmpeg err');
  console.log(err.message)	                 console.log(err.message);
  reject(err.message)	                       reject(err.message);
  })                                         })
```

ex. 2

```
if (filename != 'input.mp4')
```

ex. 3
```
const width = process.env.WIDTH;
const height = process.env.HEIGHT;
const URL = process.env.URL;
const newBucket = process.env.NEW_BUCKET;
const framerate = process.env.FRAMERATE
const ALLOWED_RESOLUTIONS = process.env.ALLOWED_RESOLUTIONS ? new 
```

#### Databases

The artifact I chose for this milestone is the same artifact that I chose for Software Design/Engineering; the Vue.js front-end and flat-file content management system associated with [brightbluewaves.com](https://brightbluewaves.com). This artifact is [open-source](https://github.com/cgberlin/brightbluewaves). My plan with this artifact in regard to enhancing/improving functionality which fit the “databases” category was to fix the “contact me” button so that it would actually submit a form rather than just try to open a mailto link. Originally I was planning to host my own “serverless contact form” API, but due to time constraints and Netlify deciding to launch their own [identical product](https://www.netlify.com/products/forms/) I opted for integrating theirs. This fit within the “serverless” theme of the site, with the entire content management system, file/media storage, analytics, and now even the contact form being handled without a backend API or infrastructure. 

Databases are an interesting topic, and I have extensive professional experience scaling everything from MongoDB to PostreSQL instances and architectures. The reason that the contact form fit within the “databases” prompt is because it inherently requires one to function. Somewhere there is a relation from my site and domain to the SMTP forwarding server, and that relation must be stored in a database somewhere. The idea of “serverless” architectures is misleading and, in my opinion, often a misnomer. All this functionality inherently requires servers and databases to work; we used to have to host them ourselves but now with the rise of the “cloud” we can simply let other people host them for us. 

I am happy with the result and how the final project turned out. Not only do I think it will functionally work for my father’s use cases, but learning how and being able to offload the scaling and underlying infrastructure to Netlify and Forestry has relieved me of the a lot of the long-term maintenance worries that used to bug me with personally-hosted projects for other people. Getting Netlify to place nicely with a Vue.js controlled contact form was not a walk in the park, and I am thankful that I now have code to re-use in the future. Due to how I had to test this (write change, commit, push, let netlify build, test live) the commits are pretty spread out but all took place today on [February 6th](https://github.com/cgberlin/brightbluewaves/commits/master)

### Security

Both of these projects passively offer excellent security through offloading of responsibility. Due to their cloud-based nature, with both artifacts being completely serverless (the lambda is hosted by AWS and brightbluewaves.com by Forestry/Netlify), security becomes as simple as key, deployment, and database management. 


### Contact

My updated contact info/where I'm working/what I am doing is available 24/7 at [codyberlin.com](https://codyberlin.com)
