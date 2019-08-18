FROM redis:4
ENV REDIS_PASSWORD fjjUIJIdui892ji89JJIShu
COPY ./redis.conf /usr/local/etc/redis/redis.conf
CMD ["sh", "-c", "exec redis-server  \/usr\/local\/etc\/redis\/redis.conf --requirepass \"$REDIS_PASSWORD\""]
