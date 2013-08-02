fork form https://github.com/nostra13/Android-Universal-Image-Loader/tree/master/library v1.8.5

private void initImageLoader()
    {
        ImageLoaderConfiguration config = new ImageLoaderConfiguration.Builder(getApplicationContext())
            .threadPoolSize(2).threadPriority(Thread.NORM_PRIORITY - 2)
            .memoryCacheSize((int)(2 * 1024 * 1024))
            .denyCacheImageMultipleSizesInMemory()
            // .offOutOfMemoryHandling()
            .memoryCache(new UsingFreqLimitedMemoryCache(2 * 1024 * 1024))
            .tasksProcessingOrder(QueueProcessingType.LIFO)
            // .discCacheSize(50 * 1024 * 1024)
            .discCacheDir(VideoConstants.Path.IMAGE_CACHE_PATH)
            .discCacheFileNameGenerator(new Md5FileNameGenerator())
            .userAgent(VideoConstants.UserAgent)
            // .enableLogging()
            .build();

        // Initialize ImageLoader with configuration.
        ImageLoader.getInstance().init(config);
    }



 mImageLoader = ImageLoader.getInstance();
        mMemoryCache = mImageLoader.getMemoryCache();
        mOptions = new DisplayImageOptions.Builder()
            .showStubImage(R.drawable.transparent)
            .cacheInMemory()
            .cacheOnDisc()
            .imageScaleType(ImageScaleType.IN_SAMPLE_INT)
            .build();


  private void displayImage(ImageView imageView, String url)
    {
        Bitmap bitmap = mMemoryCache.get(url);
        if (bitmap != null && !bitmap.isRecycled())
        {
            imageView.setImageBitmap(bitmap);
        }
        else
        {
            mImageLoader.displayImage(url, imageView, mOptions, null);
        }
    }