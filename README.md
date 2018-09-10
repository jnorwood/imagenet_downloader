# imagenet_downloader
Download ImageNet images from list of IDs and URLs

I modified this so that it works on ubuntu 18.04 and anaconda installation of tensorflow, with python 3.6
It fixes the few minor issues with urllib replacing urllib2 from the original.
I tried this later on windows, and found that the urllib.error.HTTPError didn't exist, but didn't try to debug the issue.

One other improvement would be to shuffle the input list, if you are trying to get images from each category.
I'm doing that now in ubuntu with:
sort -R ilsvrc12_urls.txt >ilsvrc12_urls_rand.txt
and then running with the ilsvrc12_urls_rand.txt as input

I'm normally running inside vscode debug, and I haven't figured out where to set commandline input there yet, so
I just modify the parse_args call to hard-code in the command-line input strings.
   args = p.parse_args()
   args = p.parse_args(['/home/jay/img/ilsvrc12_urls_rand.txt', '/home/jay/img', '--jobs', '4', '--retry',  '3', '--sleep', '1', '-v'])

I also found that the original 100 jobs setting was too high for me.
Most of the links request .jpg, but I noticed that in some cases we get .png files back from flickr with an error message.
I'd estimate over 80% of the 2882 requested .png files are errors, so I'd suggest excluding them.
Maybe the same for the relatively small number of .gif files.
