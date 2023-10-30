# PHP File Uploader Class

The PHP File Uploader Class simplifies the process of uploading files to a server directory. It includes error handling for common upload issues, file type validation, and size checks. You can easily integrate this class into your web applications for file uploads.

## Features

- Upload files to a specified directory.
- Checks for valid file extensions (supports common image formats by default).
- Handles common upload errors and provides detailed error messages.

## Usage

1. Include the `FileUploader` class in your PHP file.

```php
require_once 'FileUploader.php';

1. Create an instance of the FileUploader class, specifying the HTML input name for the file and the target upload directory.

$fileUploader = new FileUploader('your_input_name', 'your_upload_directory');


1. Use the upload method to handle the file upload. It will return success messages or error messages, which you can display in your application.

echo $fileUploader->upload();


1. You can adjust the accepted file extensions and maximum file size according to your project's requirements.
Requirements
PHP 5.6 or higher.
License
This project is licensed under the MIT License - see the LICENSE file for details.

Acknowledgments
This class simplifies the process of handling file uploads in PHP applications, making it easy to integrate file upload functionality into your projects.
Feel free to customize this README to better suit your project's specific details and usage instructions. Make sure to provide clear and concise information to help others understand how to use your PHP File Uploader Class.




