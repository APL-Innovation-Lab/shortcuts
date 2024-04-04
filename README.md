# Integrating with Austin Public Library Drupal Site API

This guide aims to assist developers and content managers in interacting with the Austin Public Library's Drupal site via the API, enabling both read and write operations in a programmatic manner. We'll start with a simple GET request to fetch the latest article and then discuss how to set up posting content via a POST request.

## Prerequisites

For read-only operations (GET requests), you can start right away without any special setup. However, if you wish to perform write operations (POST requests), you'll need:

- An **API key** for authentication with the Austin Public Library's Drupal site. To obtain an API key, contact [bryce.benton@austintexas.gov](mailto:bryce.benton@austintexas.gov).
- The iOS Shortcuts app installed on your device.

## Fetching the Latest Article (GET Request)

To simply fetch and display the latest article from the Austin Public Library site, follow these steps to create an iOS shortcut:

1. **Open the Shortcuts App**: Launch the Shortcuts app on your iOS device.
2. **Create a New Shortcut**: Tap the "+" button to begin.
3. **Add a 'Get Contents of URL' Action**:
    - Set the action to perform a GET request.
    - For the URL, use an endpoint like `https://library.austintexas.gov/aplapi/node/article?sort=-created`, assuming articles are returned in reverse chronological order.
4. **Extract and Display the Article**:
    - Add actions to parse the JSON response and display the title or content of the latest article.

### Displaying the Title of the Latest Article

After you have fetched the latest article using a GET request, to display its title, you will need to parse the JSON response. This involves a series of steps to drill down through the JSON structure to extract the title. The structure you'll navigate is `data` -> first item -> `attributes` -> `title`. Here's how to set it up in your iOS Shortcut:

1. **Add 'Get Dictionary from Input' Action**:
    - Place this action right after your 'Get Contents of URL' action. This will parse the incoming JSON response into a format that the Shortcuts app can interpret and manipulate.
2. **Extract the First Article**:
    - The articles are typically returned in an array format under the `data` key. To access this array, add a 'Get Dictionary Value' action, specifying the key as `data`.
    - To retrieve the first article from this array, indicating the latest one, add a 'Get Item from List' action afterward, set to get the first item.
3. **Navigate to the Article's Attributes**:
    - Now that you have the first article, you need to access its attributes. Add another 'Get Dictionary Value' action, this time specifying the key as `attributes`. This will let you access the properties of the article, including its title.
4. **Get the Article Title**:
    - After accessing the attributes, add one more 'Get Dictionary Value' action to extract the title. Set the key to `title` to retrieve the article's title.
5. **Display the Title**:
    - With the title extracted, use a 'Show Result' action to display it. You can customize the text to say something like "Latest Article Title: " followed by the variable that holds the title.
6. **Name and Save Your Shortcut**.

This step-by-step guide helps ensure you can display the title of the latest article by correctly parsing the JSON response according to the specified structure: `data` -> first item -> `attributes` -> `title`.

## Posting Content (POST Request)

For posting content, like creating a new article, follow the prerequisite steps to obtain an API key and then configure your shortcut for a POST request:

1. **Launch the Shortcuts App** and create a new shortcut.
2. **Set Up a 'Get Contents of URL' Action for POST**:
    - Choose POST as the method.
    - Input the endpoint URL for creating content.
3. **Configure Headers for API Key Authentication**:
    - Add a Header where the key is `Authorization` and the value is your API key, or follow the specific authentication method required by the library's Drupal site.
4. **Set Up the POST Body**:
    - Choose JSON as the body type and configure it with the necessary fields to create an article. For example:
      ```json
      {
        "type": "node--article",
        "title": "Your New Article Title",
        "body": {
          "value": "Content of the article.",
          "format": "plain_text"
        }
      }
      ```
5. **Handling the Response**:
    - Parse and display the response to ensure the content was posted successfully.

## Further Notes

- **GET Requests**: No API key is needed for reading content.
- **POST Requests**: Contact Bryce Benton for an API key if you intend to write content.
- **Security**: Keep your API key confidential to prevent unauthorized access.

This documentation is designed as a starting point and will continue to evolve with contributions from the community. If you have successfully created a shortcut or have tips to help others, please consider contributing to the relevant sections of this guide.

# Austin Public Library iOS Shortcuts

Welcome to the Austin Public Library iOS Shortcuts repository! This repository is designed to showcase and provide educational resources on creating and modifying iOS Shortcuts to access data from the Austin Public Library's Drupal website at [library.austintexas.gov](https://library.austintexas.gov/).

## Table of Contents

- [Introduction](#introduction)
- [Getting Started](#getting-started)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Available Shortcuts](#available-shortcuts)
- [Creating Custom Shortcuts](#creating-custom-shortcuts)
- [Modifying Existing Shortcuts](#modifying-existing-shortcuts)
- [Contributing](#contributing)
- [License](#license)

## Introduction

iOS Shortcuts is a powerful tool that allows users to automate tasks and create personalized workflows on their iOS devices. This repository focuses on leveraging iOS Shortcuts to interact with the Austin Public Library's website, enabling users to access library data, perform searches, and retrieve information easily.

## Getting Started

To get started with using and creating iOS Shortcuts for the Austin Public Library, follow the instructions below.

### Prerequisites

- An iOS device running iOS 12 or later
- The Shortcuts app installed on your device

### Installation

1. Open the Shortcuts app on your iOS device.
2. Browse the available shortcuts in this repository.
3. Tap on a shortcut you want to install.
4. Tap the "Get Shortcut" button to add the shortcut to your library.

## Available Shortcuts

This section will be updated with a list of available shortcuts and their descriptions as they are developed and contributed by the community.

## Creating Custom Shortcuts

This section will provide tutorials and examples to guide you through the process of creating custom shortcuts using the Shortcuts app. If you have successfully created a shortcut or have tips to help others, please consider contributing to this section!

For a starting point, check out the guide on [Fetching the Latest Article](#fetching-the-latest-article-get-request) as an example of creating a custom shortcut.

## Modifying Existing Shortcuts

Instructions on how to modify and enhance existing shortcuts will be added here. If you have found ways to improve the shortcuts in this repository, please share your knowledge by contributing to this section.

## Contributing

We welcome contributions from the community! If you have created a useful shortcut, have an idea for improving an existing one, or want to help write the documentation, please feel free to submit a pull request. Make sure to follow the [Contributing Guidelines](CONTRIBUTING.md) when submitting your changes.

## License

This repository is licensed under the [MIT License](LICENSE). You are free to use, modify, and distribute the shortcuts in this repository as per the terms of the license.
