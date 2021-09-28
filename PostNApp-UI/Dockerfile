FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build

WORKDIR /app/src

COPY PostN.DataAccess/*.csproj PostN.DataAccess/
COPY PostN.Domain/*.csproj PostN.Domain/
COPY Tests/*.csproj Tests/
COPY PostN.WebApi/*.csproj PostN.WebApi/

COPY *.sln ./
RUN dotnet restore

COPY . ./

RUN dotnet publish --configuration Release --no-restore -o ../dist PostN.WebApi

FROM mcr.microsoft.com/dotnet/aspnet:5.0

WORKDIR /app

COPY --from=build /app/dist ./

#ENV ConnectionStrings__SqliteEmailDb "Data Source=email.db"

CMD [ "dotnet", "PostN.WebApi.dll" ]

#HEALTHCHECK CMD curl --fail http://localhost/health || exit
