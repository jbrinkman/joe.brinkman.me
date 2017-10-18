---
{
    Title: "Serverless Blogging",
    Published: "10/17/2017",
    Tags: ["Blog","Serverless","GitHub"]
}
---

# Overview

Serverless computing is all the rage today. Services like AWS Lambda and Azure Functions allow you to build applications without worrying about where your code runs or when to scale up and down the resources for your application. While there is a server somewhere that is running your code, you don't have to worry about it.  All of the server management details are handled for you and you can focus your effort on just your code.

# Evaluating My Options

As I was evaluating different blogging options I shortlisted the features I wanted:

1. Blogging - must support blogging (posting, commenting, RSS)
1. Full Control - can change any aspect I choose
1. Low maintenance - operates with little to no intervention
1. Lightweight - doesn't have hundreds of unneeded features
1. Flexible - the system could be extended if needed. Bonus points if I had the knowledge to create extensions.
1. Scalable - should be easy to host and handle almost unlimited load

In evaluating systems I looked at three different types of systems. CMS platforms like DNN, Drupal and Wordpress are generally very flexible and scalable systems that could easily handle my blogging needs. The one area where these tools fall short is that they all have hundreds of features that overkill if you are just looking for a blog. Each of these features steals CPU cycles and creates a potential security risk. This results in needing higher end hosting resources which means I would be spending more time on maintaining the system rather than focusing on the blog. As anyone who has ever had to drop everything to upgrade their site due to a security issue knows, this is not an insignificant issue.

The second set of systems I looked at are dedicated blogging platforms. In recent years, the number of blogging platforms has been shrinking. The only real option that I see today is Ghost or Medium. While both of these are well established options I didn't feel that I would have the necessary control if I went with Medium and I felt like the maintenance costs for Ghost would still be a bit high.

The final set of systems I considered were static site generators. Site generators are interesting to me since they ultimately just aid in creating static HTML sites. HTML sites are about as scalable as you can get since all of the content can be cached and there is no server processing needed to serve the content. With some of the hosting options available, I could serve up the site for almost no cost. Most of the site generators I evaluated supported extensible generation pipelines and some sort of markdown or scripting language for controlling the visual aspects of the site.

The site generation option ticked off every feature on my wish list.

# Picking a Site Generator

A couple years ago, Phil Haack began [hosting his blog on GitHub](http://www.shopsmith.com/ownersite/catalog/l_univlathetoolrest.htm). This really intrigued me. By hosting on GitHub, Phil completely eliminated his maintenance efforts. GitHub serves up millions of pageviews every day so my few page views won't even be noticed. Even a twitter mention by [Scott Hanselman](https://www.hanselman.com/) won't be enough to swamp my blog with traffic. GitHub definitely looked like a good, albeit unusual, hosting option. And it is totally free which means that the wife acceptance factor is very high.

There are many great [static site generators](https://www.staticgen.com/) to choose from. I knew that there would be one that was just right for my purposes.

The GitHub Pages feature that I would be leveraging to host my blog is nice. It includes full support for Jekyll, a very popular static site generator. Unfortunately, Jekyll is written in Ruby.  While that was not a deal killer, it added a bit of friction to getting started, and would potentially complicate things whenever I wanted to extend the platform. I had previous experience building a site in [Sphinx](http://www.sphinx-doc.org/en/stable/) and Python, and I learned the hard way that learning a new language and a new tool is a big task that complicates the site building process. I have worked in many different programming languages, but Ruby is not one of them so I wanted to avoid Jekyll for this project if I could.

After exploring a handful of different static generators, I finally settled on [Wyam](http://wyam.io) as being the best fit for me. Not only is it written in .Net (C#), the project appears to be [actively maintained](https://github.com/Wyamio/Wyam) and the author is very responsive to [questions on Gitter](https://gitter.im/Wyamio/Wyam).

Wyam is very similar to most generators I evaluated. It includes support for creating my own themes. In Wyam Themes are built using Razor Pages. This allows me to use all of my ASP.Net skills for hand-crafting my own custom theme. Although Wyam includes five different built-in themes out of the box, I much prefer to craft my own theme so that my site reflects my personal tastes.

On the content side Wyam includes standard support for creating my pages with markdown. This makes it easy to create content without a lot of fuss. When I need a little more control over the final markup, I can always create my pages using Razor script. This gives me the full power of HTML and C# so I can get as fancy as I want for those few pages where the extra control may be necessary.

All document generation in Wyam is the result of running a set of input files through a number of pre-written pipelines. These pipelines take the input files and generate the HTML, CSS and JavaScript for my final site. In Wyam these pipelines are called recipes. Out of the box there are recipes for Blogs, BookSites and Documentation Sites. With support for markdown, Razor, LESS, SASS, JSON and YAML, I have just about everything I need to create beautiful sites. Of course, if the built-in recipes don't suit my needs, I can easily craft my own or customize the pre-built recipes to suit my particular needs. If desired I could easily extend Wyam to include support for [Liquid markup](http://dotliquidmarkup.org/), add support for frontmatter written in XML or any number of interesting customizations. I am in complete control, and I don't have to make any changes to the core Wyam platform to make these enhancements. That is exactly the kind of control that I was looking for.

# Just a Few Comments

The heart of the blogging experience focuses on publishing articles. This is a task that any decent static site generator can handle with ease. But a blog is about more than just publishing articles. It is about engaging in a conversation with your readers. It is about expressing your views, sharing your knowledge and then interacting with your readers to get their viewpoint. Commenting then becomes the soul of your blog. It is where your ideas meet the real world and are challenged or confirmed.

# Performance and Security

# Wrapping it Up