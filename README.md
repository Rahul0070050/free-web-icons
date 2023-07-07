# VS Code Extension: Free Icons

## Overview
This Visual Studio Code extension provides access to all versions of Font Awesome icons. With this extension, you can search for any icon you want, select specific versions, and easily copy icons and their corresponding CDN links.

## Features
- Search: Easily search for any Font Awesome icon using keywords or names.
- Version Selection: Choose specific versions of Font Awesome icons to ensure compatibility with your projects.
- Copy Icons: Quickly copy the selected icon's HTML code or CSS class to use in your code.
- Copy CDN: Copy the CDN link for the selected Font Awesome version to include in your HTML files.

## Installation
1. Launch Visual Studio Code.
2. Go to the Extensions view (Ctrl+Shift+X) or click on the square icon in the left sidebar.
3. Search for "Free Web Icons" or "rahulor (author name)" and click on the extension with the same name.
4. Click the "Install" button to install the extension.
5. Once installed, the extension will be ready for use.

## Usage
1. Open a new or existing HTML file in Visual Studio Code.
2. Click on the "Free Web Icons" extension icon in the sidebar (represented by the Smiley logo).
3. The extension panel will appear on the side of the editor.
4. In the search bar, enter the name or keywords of the icon you want to find.
5. Select the desired version of Font Awesome from the dropdown menu.
6. The search results will display matching icons based on your search criteria.
7. Click on an icon to copy its HTML code to your clipboard.
8. If needed, click the "Link" button to copy the corresponding Font Awesome CDN link to your clipboard.

Great! With the provided repository link, here's the updated "Contributing" section for your project's README file:

## Contributing

Thank you for your interest in contributing to Free Web Icons! Your contributions help improve the project and make it more valuable for the community. You can contribute by adding icons to the project's extension. Please follow the guidelines below.

### Getting Started

To get started with contributing icons to the Free Web Icons extension, follow these steps:

1. Fork the repository by clicking the "Fork" button at the top right corner of the [Free Web Icons repository](https://github.com/Rahul0070050/free-web-icons).
2. Clone your forked repository to your local machine:
   ```
   git clone https://github.com/Rahul0070050/free-web-icons.git
   ```
3. Navigate to the following files in the cloned repository:
   - `webview/media/data/fa-icons.json`
   - `webview/media/data/versions.json`

### Adding Icons

To add icons to the extension, follow these steps:

1. Open the `fa-icons.json` file in a text editor.
2. Find the section corresponding to the category or group you want to add icons to.
3. Add an icon entry in the following format:
   ```json
   {
       "name": "Icon Name",
       "showIcon": "fa-icon-class",
       "variants": []
   }
   ```
   Replace `"Icon Name"` with the name of the icon and `"fa-icon-class"` with the appropriate class or code for the icon.

4. Open the `versions.json` file in a text editor.
5. Add the version numbers of the extension in the following format:
   ```json
   [
       "6.4.0",
       "5.15.4"
   ]
   ```
   Include the appropriate version numbers for the extension.

### Submitting Your Changes

Once you have added the icons and updated the version numbers, follow these steps to submit your changes:

1. Create a new branch for your changes:
   ```
   git checkout -b add-icons
   ```

2. Commit your changes:
   ```
   git add webview/media/data/fa-icons.json webview/media/data/versions.json
   git commit -m "Add icons and update versions"
   ```

3. Pull the latest changes from the remote repository to ensure your branch is up to date:
   ```
   git pull origin master
   ```

4. Push your branch to your forked repository:
   ```
   git push origin add-icons
   ```

5. Open a pull request (PR) on the original repository:
   - Go to the [Free Web Icons repository](https://github.com/Rahul0070050/free-web-icons) on GitHub.
   - Click on the "Pull requests" tab.
   - Click the "New pull request" button.
   - Provide a clear title and description for your pull request, explaining the icons you added.
   - Select your branch (`add-icons`) as the compare branch.
   - Submit the pull request.

### Code Review and Feedback

Your pull request will be reviewed by the project maintainers. They may provide feedback, suggest changes, or request additional information. Please be responsive to the feedback and make any necessary updates or improvements.

Thank you for contributing to Free Web Icons! Your efforts in expanding the collection of icons are greatly appreciated.

---

Feel free to customize this section further to fit your project's specific guidelines and requirements.

## Credits

This extension utilizes icons from Font Awesome (free version) to enhance the user interface.

Font Awesome offers a comprehensive collection of high-quality scalable icons that can be easily customized and used in various projects. The free version provides a wide range of icons that can add visual appeal and clarity to your application.

To learn more about Font Awesome and explore their collection of icons, please visit their official website: [Font Awesome](https://fontawesome.com/)

We would like to express our gratitude to the Font Awesome team for providing the free version, enabling us to incorporate their icons into our extension.

## Release Notes
### Version 0.0.6
 - icons added to the extension

