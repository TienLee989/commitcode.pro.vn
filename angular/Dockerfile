# Bước 1: Sử dụng hình ảnh Node.js 16.15 làm môi trường build
FROM node:16.15.0 AS build

# Thiết lập thư mục làm việc
WORKDIR /app

# Sao chép package.json và package-lock.json vào thư mục làm việc
COPY package*.json ./

# Cài đặt các phụ thuộc
RUN npm install

# Sao chép mã nguồn vào thư mục làm việc
COPY . .

# Build ứng dụng Angular
RUN npm run ng -- build

# Bước 2: Sử dụng hình ảnh Nginx để phục vụ ứng dụng
FROM nginx:alpine

# Sao chép build artifacts từ bước build vào thư mục Nginx
COPY --from=build /app/dist/ngx-admin-demo /usr/share/nginx/html

# Expose cổng 80 cho Nginx
EXPOSE 80

# Khởi động Nginx
CMD ["nginx", "-g", "daemon off;"]
