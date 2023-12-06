# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0.100 AS build-env
ARG NO_CACHE

WORKDIR /PieApp
COPY . ./
RUN dotnet --version
RUN dotnet restore
RUN dotnet publish -c Release -o out $NO_CACHE

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /PieApp
COPY --from=build-env /PieApp/out .

# Use the same stage as runtime for the final image
ENTRYPOINT ["dotnet", "PieApp.dll"]
# Final stage
FROM runtime AS final
ENTRYPOINT ["dotnet", "PieApp.dll"]