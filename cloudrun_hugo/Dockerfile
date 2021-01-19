FROM klakegg/hugo:0.52 as builder
WORKDIR /app
ADD . ./
RUN hugo
RUN chmod 777 minify_linux
RUN ./minify_linux -r -v --match=\.*html --html-keep-document-tags -o public public
RUN ./minify_linux -r -v --match=\.*css --html-keep-document-tags -o public public
RUN ./minify_linux -r -v --match=\.*js --html-keep-document-tags -o public public

FROM nginx:alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/public /usr/share/nginx/html/
