# Gunakan nginx alpine sebagai base image
FROM nginx:alpine

# Copy file HTML ke direktori nginx di dalam kontainer
COPY app/index.html /usr/share/nginx/html/index.html

# Beritahu Docker bahwa aplikasi berjalan di port 80
EXPOSE 80

# Jalankan nginx
CMD ["nginx", "-g", "daemon off;"]