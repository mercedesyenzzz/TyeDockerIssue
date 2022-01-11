FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
EXPOSE 80
WORKDIR /app
COPY ["BlazorWasm/BlazorWasm.csproj", "Client/"]
RUN dotnet restore "Client/BlazorWasm.csproj"
COPY . .
RUN dotnet build "BlazorWasm/BlazorWasm.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlazorWasm/BlazorWasm.csproj" -c Release -o /app/publish 

FROM nginx:alpine AS final
WORKDIR /usr/share/nginx/html
COPY --from=publish /app/publish/wwwroot .
COPY ["BlazorWasm/wwwroot/nginx.conf","/etc/nginx/nginx.conf"]
