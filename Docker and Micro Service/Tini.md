#[Tini](https://github.com/krallin/tini.git) 
##key: ```Tini,孤儿进程,僵尸进程,进程接管```

##Abstraction: 
Tini is the simplest init you could think of.

All Tini does is spawn a single child (Tini is meant to be run in a container), and wait for it to exit all the while reaping(接管） zombies and performing signal forwarding.

In Docker, you will want to use an entrypoint so you don't have to remember to manually invoke Tini:
```
# Add Tini
ENV TINI_VERSION v0.10.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

# Run your program under Tini
CMD ["/your/program", "-and", "-its", "arguments"]
# or docker run your-image /your/program ...
```