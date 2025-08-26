FROM nginx:mainline

ENV LLM_CONSULTANT_WIDGET_DOMAIN=${LLM_CONSULTANT_WIDGET_DOMAIN}
ENV LLM_CONSULTANT_API_DOMAIN=${LLM_CONSULTANT_API_DOMAIN}

RUN ["rm", "/etc/nginx/conf.d/default.conf"]

# Starting an infinity loop with the 6-hour timer and after restart the nginx to maintain "Let's Encrypt"
CMD while :; do sleep 6h & wait ${!}; nginx -s reload; done & export LLM_CONSULTANT_WIDGET_DOMAIN LLM_CONSULTANT_API_DOMAIN && envsubst '$LLM_CONSULTANT_WIDGET_DOMAIN' < /etc/nginx/templates/widget-http.conf.template > /etc/nginx/conf.d/widget.conf && envsubst '$LLM_CONSULTANT_API_DOMAIN' < /etc/nginx/templates/api-http.conf.template > /etc/nginx/conf.d/api.conf && nginx -g 'daemon off;'

EXPOSE 80 443 8080