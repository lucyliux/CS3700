HIGH LEVEL APPROACH:
We first log in to fakebook by sending a get request for the tokens we need to log in. Then we make a post request with the necessary login information. Once we log in, we first search for the anchor tag in the html, and then store the buffered url in a list of buffered urls. Then we traverse through the URLS using the http get method searching for our flags and keep track of the already visited urls in a list of visited urls. This way, we do not search through a url that we have already searched through. We also handle the get response from the server accordingly. 200: return response, 302: request again with a new URL given by the server, 403/404: abandon the URl 503: try again until the request for the url is succesful.

Challenges:
Figuring out how to login properly to fakebook was difficult. We didnt know how to properly handle server responses to the tokens from the get request.
Our script also took a very long time to run, which made it a bit difficult to test.

Testing:
We ran the script multiple lines with bunch of print lines, and also tried submitting to gradescope