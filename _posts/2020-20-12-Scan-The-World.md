---
layout: post
title:  "Scan The All EDU Sites in World!"
date:   2020-12-20 06:26:01 +0300
---
# [](#header-4)What is .git Folder?

Git is a distributed version-control system for tracking changes in any set of files, originally designed for coordinating work among programmers cooperating on source code during software development. Its goals include speed, data integrity, and support for distributed, non-linear workflows. (Wikipedia)


In recent years, security researchers have seen that source code can be accessed with forgotten /.git repositories on applications.

# [](#header-4)What am I aiming for?

After the research, to determine how many of the `edu` applications found in the world have source code available. I would first make a GET /.git/config request to all edu addresses I detected. If I detect `repositoryformatversion` in the response after the request, I would save it to a file.

I needed to minimize the false positive result. So I needed a word that is unlikely to be in the page source but contained in .git/config 


{% highlight python %}
    sonurl = "https://" + url.strip() + "/.git/config"
    try:
        user_agent = 'Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)'
        request = urllib.request.Request(sonurl, headers={'User-Agent': user_agent})
        response = urllib.request.urlopen(request,context=ctx,timeout=3)
        content = str(response.read())
    except Exception as e:
        pass
    else:
        if (content.find('repositoryformatversion') != -1):
            yaz.write(sonurl + "\n")
            print("\033[1;32;40m[{}] Founded --> saved {}".format(str(th_number), str(sonurl)) + '\x1b[0m')
{% endhighlight %}

In the above code block. I would make the /.git/config request and get addresses with repositoryformatversion in the response. 
I would like to thank "Associate Professor I. Berkan Aydilek" and "Numan Turle" for their assistance in Multi Process.

# [](#header-4)Research Time!

The tool makes the request I mentioned above to edu addresses in the wordlist with 100 processes.

![](https://0x45dda458.github.io/assets/stw-1.png)

# [](#header-4)Bingoooo!

![](https://0x45dda458.github.io/assets/stw-2.jpg)

I had detected 43 systems that could expose source code in about 6 minutes.

![](https://0x45dda458.github.io/assets/stw-3.png)


Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
