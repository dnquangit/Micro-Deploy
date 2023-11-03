FROM mcr.microsoft.com/dotnet/aspnet:7.0 As base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build 
WORKDIR /src

COPY ["src/Services/Product.API/Product.API.csproj", "Services/Product.API/"]

RUN dotnet restore "Services/Product.API/Product.API.csproj"

COPY src .
WORKDIR /src/Services/Product.API
RUN dotnet build "Product.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Product.API.csproj" -c Release -o /app/publish

FROM base as final
WORKDIR /app
COPY --from=publish /app/publish .

ENTRYPOINT [ "dotnet","Product.API.dll"]

#CMD ["sleep", "infinity"]