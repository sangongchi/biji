> //跳转至yum源，添加google-chrome到源
> cd etc/yum.repos.d
>
> //编辑添加源
> vim google-chrome.repo
>
> //添加如下内容
>
> ```bash
> [google-chrome] 
> 
> name=google-chrome 
> 
> baseurl=http://dl.google.com/linux/chrome/rpm/stable/$basearch 
> 
> enabled=1
> 
> gpgcheck=1 
> 
> gpgkey=https://dl-ssl.google.com/linux/linux_signing_key.pub
> ```
>
> //之后运行： 
>
> ```bash
> yum -y install google-chrome-stable --nogpgcheck
> ```

