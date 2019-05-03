# buerguo.com
my hexo blog source


### 怎么发布？

写完md的文章后，执行以下命令
```
hexo deploy --generate
or
hexo d -g
or
hexo g -d
```

### 怎么样自定义域名？

1. *hexo g*命令以后会生成public目录，

2. 在public目录下新增*CNAME*文件，

3. 写入自定义域名*www.buerguo.com*

4. 再次发布 *hexo d*



