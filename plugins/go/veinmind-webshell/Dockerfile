FROM veinmind/go1.18:1.1.0-stretch as builder
WORKDIR /build
COPY . .
RUN sed -i 's/\.\.\/veinmind-common/\.\/veinmind-common/g' go.mod
RUN chmod +x script/build.sh && /bin/bash script/build.sh

FROM veinmind/base:1.1.0-stretch as release
WORKDIR /tool
COPY --from=builder /build/veinmind-webshell .
RUN echo "#!/bin/bash\n\n./veinmind-webshell \$*" > /tool/entrypoint.sh && chmod +x /tool/entrypoint.sh && chmod +x /tool/veinmind-webshell
ENTRYPOINT ["/tool/entrypoint.sh"]
