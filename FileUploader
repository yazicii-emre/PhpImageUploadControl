<?php

class FileUploader
{
    public $filename;
    public $uploadsDir = '/system/myimg/';
    public $filePath;

    public function __construct($filename, $filePath)
    {
        try {
            $this->filename = $filename;
            $this->filePath = $filePath;

            if ($errorMessage = $this->getUploadErrorMessage()) {
                echo $errorMessage;
            } elseif ($extensionError = $this->checkFileExtension()) {
                echo $extensionError;
            } elseif ($this->checkFileSize()) {
                echo 'File size is too large!';
            } elseif (!preg_match("`^[-0-9A-Z_\.]+$`i", $_FILES[$this->filename]['name'])) {
                echo 'Special characters are not allowed in the file name!';
            } else {
                $tmpName = $_FILES[$this->filename]["tmp_name"];
                $name = basename(strtolower($_FILES[$this->filename]['name']));
                $uploadsDir = $_SERVER['DOCUMENT_ROOT'] . $this->uploadsDir . $this->filePath;
                $fileExists = $uploadsDir . '/' . $_FILES[$this->filename]['name'];

                if (!is_file($uploadsDir)) {
                    mkdir($uploadsDir);
                }

                if (move_uploaded_file($tmpName, "$uploadsDir/$name")) {
                    echo "Your file was successfully uploaded to the $this->filePath directory.";
                }
            }
        } catch (PDOException $e) {
            return ['status' => FALSE, 'error' => $e->getMessage()];
        }
    }

    private function checkFileExtension()
    {
        try {
            $extensions = strtolower(pathinfo(basename($_FILES[$this->filename]['name']), PATHINFO_EXTENSION));
            $allowedExtensions = ['jpg', 'png', 'jpeg'];

            if (!in_array($extensions, $allowedExtensions)) {
                throw new PDOException('Invalid file extension!');
            }
        } catch (PDOException $e) {
            return $e->getMessage();
        }
    }

    private function getUploadErrorMessage()
    {
        try {
            switch ($_FILES[$this->filename]['error']) {
                case UPLOAD_ERR_INI_SIZE:
                    throw new PDOException("The uploaded file exceeds the upload_max_filesize directive in php.ini.");
                    break;
                case UPLOAD_ERR_FORM_SIZE:
                    throw new PDOException("The uploaded file exceeds the MAX_FILE_SIZE directive that was specified in the HTML form.");
                    break;
                case UPLOAD_ERR_PARTIAL:
                    throw new PDOException("The uploaded file was only partially uploaded.");
                    break;
                case UPLOAD_ERR_NO_FILE:
                    throw new PDOException("Please select a file for upload.");
                    break;
                case UPLOAD_ERR_NO_TMP_DIR:
                    throw new PDOException("Temporary folder is missing.");
                    break;
                case UPLOAD_ERR_CANT_WRITE:
                    throw new PDOException("Failed to write file to disk.");
                    break;
                case UPLOAD_ERR_EXTENSION:
                    throw new PDOException("File upload stopped by a PHP extension.");
                    break;
            }
        } catch (PDOException $e) {
            return $e->getMessage();
        }
    }
}
