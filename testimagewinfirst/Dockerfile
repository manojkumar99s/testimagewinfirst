#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see http://aka.ms/containercompat 

FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY testimagewinfirst/testimagewinfirst.csproj testimagewinfirst/
RUN dotnet restore testimagewinfirst/testimagewinfirst.csproj
COPY . .
WORKDIR /src/testimagewinfirst
RUN dotnet build testimagewinfirst.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish testimagewinfirst.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "testimagewinfirst.dll"]
