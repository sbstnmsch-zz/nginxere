# nginxere
Shell alias to ad-hoc-start up a nginx in current folder for developing and
prototyping.

# Install
Paste the following to your `.bashrc` or `.zshrc`.

```shell
alias nginxere="(which nginx > /dev/null 2>&1) && export nginxconf=$(mktemp /tmp/nginx.conf.XXXXX) && ((test -f .nginxere && (cat .nginxere|sed 's~{{=pwd}}~'$(pwd)'~g')) || (echo \"master_process off;daemon off;events{}http{types{text/html html;application/javascript js;text/css css;}access_log /dev/stdout;index index.html;server{location /{root \$(pwd);}}}\")) > \$nginxconf && echo \"Serving on http://localhost:8000\nPress CTRL-C to stop.\" && nginx -c \$nginxconf && rm \$nginxconf && echo \"\nDone.\""
```

Restart your terminal (or re-source your profile) and type `nginxere`.
A nginx is started on http://localhost:8000 or http://localhost:80 (if run as root) and
logs to `<STDOUT>`.

Happy serving.

# Custom setup
If a `.nginxere`-file exists in your project folder that one is used to run nginx.
