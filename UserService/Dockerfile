# Use the official .NET 7 SDK image as the base image
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env

# Set the working directory inside the container
WORKDIR /app

# Copy the project files to the container
COPY . ./

# Build the application
RUN dotnet publish -c Release -o out

# Label the container
LABEL maintainer="MB <mahendra.b@intelops.dev>"
LABEL repository="https://github.com/mahendraintelops/myproject"
LABEL homepage="https://github.com/mahendraintelops/myproject"

# Label as GitHub action
LABEL com.github.actions.name="The name of your GitHub Action"
# Limit to 160 characters
LABEL com.github.actions.description="The description of your GitHub Action."
# See branding:
# https://docs.github.com/actions/creating-actions/metadata-syntax-for-github-actions#branding
LABEL com.github.actions.icon="activity"
LABEL com.github.actions.color="orange"

# Use the official .NET 7 runtime image as the base image for the final image
FROM mcr.microsoft.com/dotnet/aspnet:7.0

# Set the working directory inside the container
WORKDIR /app

# Copy the published application from the build environment
COPY --from=build-env /app/out .

# Expose the port the application will run on
EXPOSE 80

# Define the entry point for the application
ENTRYPOINT ["dotnet", "UserService.dll"]
