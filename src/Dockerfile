FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env

# Set the working directory to /app
WORKDIR /app

COPY . ./hello/.
RUN dotnet publish ./hello/hello.csproj -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:7.0.5-alpine3.17 AS base
WORKDIR /app
COPY --from=build-env /app/out .

#Add users
RUN addgroup non-root-group
RUN adduser 1001 -G non-root-group -u 1001 ; echo '1001:pa55w0rd' | chpasswd
USER 1001

# Entry point for image
CMD ["hello.exe"]
