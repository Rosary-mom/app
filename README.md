# app
app for FB and Android advertisements
// In the Activity that will launch the native ad,
// implement the AdListener interface and add the following:

import com.facebook.ads.*;

private NativeAd nativeAd;

private void showNativeAd(){
  nativeAd = new NativeAd(this, "355403327897065_790340137736713");
  nativeAd.setAdListener(new AdListener() {

    @Override
    public void onError(Ad ad, AdError error) {
        ...
    }

    @Override
    public void onAdLoaded(Ad ad) {
        ...
    }

    @Override
    public void onAdClicked(Ad ad) {
        ...
    }
  });

  nativeAd.loadAd();
}

// The next step is to extract the ad metadata and use its properties 
// to build your customized native UI. Modify the onAdLoaded function 
// above to retrieve the ad properties. For example:
@Override
public void onAdLoaded(Ad ad) {
  if (ad != nativeAd) {
    return;
  }

  String titleForAd = nativeAd.getAdTitle();
  Image coverImage = nativeAd.getAdCoverImage();
  Image iconForAd = nativeAd.getAdIcon();
  String socialContextForAd = nativeAd.getAdSocialContext();
  String titleForAdButton = nativeAd.getAdCallToAction();
  String textForAdBody = nativeAd.getAdBody();
  Rating appRatingForAd = nativeAd.getAdStarRating();

  // Add code here to create a custom view that uses the ad properties
  // For example:
  LinearLayout nativeAdContainer = new LinearLayout(this);
  TextView titleLabel = new TextView(this);
  titleLabel.setText(titleForAd);
  nativeAdContainer.addView(titleLabel);
  ...

  // Add the ad to your layout
  LinearLayout mainContainer = (LinearLayout)findViewById(R.id.MainContainer);
  mainContainer.addView(nativeAdContainer);

  // Register the native ad view with the native ad instance
  nativeAd.registerViewForInteraction(nativeAdContainer);

