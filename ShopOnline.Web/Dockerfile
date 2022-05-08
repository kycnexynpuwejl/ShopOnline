#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ShopOnline.Web/ShopOnline.Web.csproj", "ShopOnline.Web/"]
COPY ["ShopOnline.Models/ShopOnline.Models.csproj", "ShopOnline.Models/"]
RUN dotnet restore "ShopOnline.Web/ShopOnline.Web.csproj"
COPY . .
WORKDIR "/src/ShopOnline.Web"
RUN dotnet build "ShopOnline.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ShopOnline.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ShopOnline.Web.dll"]
