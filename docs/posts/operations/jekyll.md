## 1. 官方Docker使用

[jekyll-docker官方文档](https://github.com/envygeeks/jekyll-docker/blob/master/README.md)

拉取镜像

```bash
docker pull jekyll/jekyll
```

创建项目

```bash
export site_name="my-blog"
docker run --rm \
  --volume="$PWD:/srv/jekyll" \
  -it jekyll/jekyll \
  sh -c "chown -R jekyll /usr/gem/ && jekyll new $site_name" \
  && cd $site_name
```

本地启动项目，启动时，目录在 `$site_name/`目录下

```bash
docker run --rm \
  --volume="$PWD:/srv/jekyll:Z" \
  --publish 4000:4000 \
  jekyll/jekyll \
  jekyll serve
```



## 2. GitBook 主题

直接下载，按下面修改 `_config.yml` 

```ruby
url:              'https://happymakerc.github.io'
baseurl:          '/'
```

如果要在本地运行，还要修改 `Gemfile` 中`source`为

```ruby
source "https://gems.ruby-china.com"
```

