### Serving Compressed files in CloudFront:

The explanation from amazon docs are very good for the compression part, so I am going with them.

You can configure CloudFront to automatically compress files of certain types and serve the compressed files when viewer requests include **Accept-Encoding: gzip** in the request header. When content is compressed, downloads are faster because the files are smaller—in some cases, less than a quarter the size of the original. Especially for JavaScript and CSS files, faster downloads translates into faster rendering of web pages for your users. In addition, because the cost of CloudFront data transfer is based on the total amount of data served, serving compressed files is less expensive than serving uncompressed files.

**Note:**

- A viewer request must include **Accept-Encoding: gzip** in the request header, or CloudFront won't compress the requested file. All modern browsers include this header by default. Doing so, will give the browsers the compressed file.

- CloudFront compresses only some file types. If you want to compress other files that CloudFront does not compress, you can do it in origin. But you have to do only in Gzip, because CF does not accept any other compression algorithms. When your origin returns the compressed file to CloudFront, it will include a Content-Encoding: gzip header, which indicates to CloudFront that the file is already compressed.
