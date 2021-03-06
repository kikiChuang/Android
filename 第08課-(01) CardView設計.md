# 第08課 CardView設計


## (1) CardView設計


##### 執行結果:
![GitHub Logo](/images/results08-1.jpg)



##### 模擬器
```
Nexus 5, API 23
```



##### 建立專案設定
```
(1) Company Domain: abc.com 
(2) Minimum SDK: API 21: Android 5.0(Lollipop)
(3) 選用 Basic Activity
```



##### 檔案放置方式:
```
 app 
   |___<res>
   |     |___<drawable>
   |     |      |___picture_1.jpg    (尺寸: 600px*400px)	
   |     |      |___picture_2.jpg    (尺寸: 600px*400px)
   |     |      |___picture_3.jpg    (尺寸: 600px*400px)   
   |     |    
   |     |___<layout>
   |     |      |___content_main.xml
   |     | 	 
   |     |___<values>
   |            |___colors.xml  
   |            |
   |            |___<dimens.xml(2)> 
   |            |        |___dimens.xml  
   |            |
   |            |___strings.xml
   |
   |___<Gradle Scripts>
                |___build.gradle(Module: app)		 
```



##### 檔案名稱: build.gradle
```xml
apply plugin: 'com.android.application'

android {
    compileSdkVersion 25
    buildToolsVersion "23.0.2"

    defaultConfig {
        applicationId "com.abc.myapplication"
        minSdkVersion 21
        targetSdkVersion 25
        versionCode 1
        versionName "1.0"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    //---------------------- 
    // 增加
    //----------------------
    compile 'com.android.support:cardview-v7:25.0.+'
    compile 'com.android.support:recyclerview-v7:25.0.+'

    compile fileTree(dir: 'libs', include: ['*.jar'])
    testCompile 'junit:junit:4.12'
    compile 'com.android.support:appcompat-v7:25.0.1'
    compile 'com.android.support:design:25.0.1'
}

```



##### 檔案名稱: colors.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="colorPrimary">#550000</color>
    <color name="colorPrimaryDark">#000</color>
    <color name="colorAccent">#550000</color>
    <color name="windowBackground">#fff</color>
    <color name="textColor">#fff</color>
    <color name="cardBack">#ffdede</color>
</resources>
```



##### 檔案名稱: dimens.xml
```xml
<resources>
    <!-- Default screen margins, per the Android Design guidelines. -->
    <dimen name="activity_horizontal_margin">5dp</dimen>
    <dimen name="activity_vertical_margin">10dp</dimen>
    
    <!-- fab按鈕位置設定 -->
    <dimen name="fab_margin">6dp</dimen>
    <dimen name="fab_marginBottom">40dp</dimen>

    <!-- 卡片尺寸設定 -->
    <dimen name="textSize">18dp</dimen>
    <dimen name="spaceVertical">6dp</dimen>
    <dimen name="textMargin">10dp</dimen>
    <dimen name="cardHeight">350dp</dimen>
    <dimen name="imageHeight">200dp</dimen>
    <dimen name="cardBottomMargin">20dp</dimen>
    <dimen name="cardCornerRadius">5dp</dimen>
</resources>
```



##### 檔案名稱: strings.xml
```xml
<resources>
    <string name="app_name">卡片測試</string>
    <string name="action_settings">Settings</string>
    <string name="logo">商標圖示</string>

    <string name="card_text_1">
        "蔣勳曾說自己是用佈道的心情傳播對美的感動，現在他已經可說是美的宗教家。近幾年來，蔣勳走遍竹科與各地演講，到場的聽眾們彷彿都期待受到「開釋」，除了在席間對於充滿抑揚頓挫的感性分析頻頻點頭，發問的許多也都是已超乎美學的人生之問。事實上，這幾年來，蔣勳談的美，也有很大的變化。他過去比較偏向幫助大家賞析藝術之美，但他在與聽眾愈來愈多的互動中發現，許多上班族的餘暇時間已極度有限了，刻意附庸風雅地去欣賞音樂會、畫展已經沒有必要，重拾與周遭人的感情，重新找回「像個人樣」的生活方式，才能對美真正有所體會。本期美學學院專訪蔣勳，分享上班族也可以找回的生活之美。"
    </string>

    <string name="card_text_2">
        "幾年來，幾乎所有的竹科企業我都去過了，和企業的人有所接觸後，我才知道我過去有「知識偏執」的狀況，但我並沒有真正認識30歲上下的職場工作人員。竹科有一家上市公司的員工平均年齡是31.8歲，他們都是最優秀大學畢業的菁英。 在開始工作的前10年，是人生很重要的階段，但他們卻通常是11點以後才下班。要戀愛，可能沒有時間戀愛；要買房子，就用世俗的固定模式買房子，找一個大家認為有名的設計師；要結婚，但用很草率的方式結婚。我知道很多工程師經由輔導去娶烏克蘭新娘，他們可能連戀愛的時間、耐心都沒有。"
    </string>

    <string name="card_text_3">
        "我現在不問工程師有沒有去聽音樂、看展覽，反而是問他們：「你們在這裡工作5年了，有沒有人可以告訴我公司門口那一排是什麼樹？」但很少人能夠回答的出來。事實上，他們公司門口那排小葉欖仁的葉子漂亮得不得了，綠色會在陽光裡發亮。後來我再去，就有一個員工和我說，「謝謝你告訴我這件事，我現在下班時會先看看小葉欖仁再回家，所以比較不會和太太吵架了。」他也問我現在5歲的女兒將來該學鋼琴、還是小提琴，但我建議11點下班的他多抱抱女兒，比較重要。"
    </string>
</resources>
```



##### 檔案名稱: content_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_marginTop="55dp"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:orientation="vertical"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:paddingBottom="@dimen/activity_vertical_margin"
    tools:context=".MainActivity">

    <!-- 加入幾張 CardViews -->
    <!-- ............................................... -->
    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical">

            <!-- 第 1 張 CardView -->
            <android.support.v7.widget.CardView
                xmlns:card_view="http://schemas.android.com/apk/res-auto"
                android:id="@+id/card_view"
                android:layout_gravity="center"
                android:layout_width="match_parent"
                android:layout_height="@dimen/cardHeight"
                android:layout_marginBottom="@dimen/cardBottomMargin"
                card_view:cardCornerRadius="@dimen/cardCornerRadius">

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:background="@color/cardBack"
                    android:orientation="vertical">

                    <ImageView
                        android:layout_width="match_parent"
                        android:layout_height="@dimen/imageHeight"
                        android:scaleType="centerCrop"
                        android:src="@drawable/picture_1"/>

                    <TextView
                        android:id="@+id/info_text"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:layout_margin="@dimen/textMargin"
                        android:lineSpacingExtra="@dimen/spaceVertical"
                        android:background="@color/cardBack"
                        android:textSize="@dimen/textSize"
                        android:text="@string/card_text_1" />

                </LinearLayout>
            </android.support.v7.widget.CardView>


            <!-- 第 2 張 CardView -->
            <android.support.v7.widget.CardView
                xmlns:card_view="http://schemas.android.com/apk/res-auto"
                android:id="@+id/card_view2"
                android:layout_gravity="center"
                android:layout_width="match_parent"
                android:layout_height="@dimen/cardHeight"
                android:layout_marginBottom="@dimen/cardBottomMargin"
                android:background="@color/cardBack"
                card_view:cardCornerRadius="@dimen/cardCornerRadius">

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:background="@color/cardBack"
                    android:orientation="vertical">

                    <ImageView
                        android:layout_width="match_parent"
                        android:layout_height="@dimen/imageHeight"
                        android:scaleType="centerCrop"
                        android:src="@drawable/picture_2"/>

                    <TextView
                        android:id="@+id/info_text2"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:layout_margin="@dimen/textMargin"
                        android:lineSpacingExtra="@dimen/spaceVertical"
                        android:textSize="@dimen/textSize"
                        android:text="@string/card_text_2" />
                </LinearLayout>
            </android.support.v7.widget.CardView>


            <!-- 第 3 張 CardView -->
            <android.support.v7.widget.CardView
                xmlns:card_view="http://schemas.android.com/apk/res-auto"
                android:id="@+id/card_view3"
                android:layout_gravity="center"
                android:layout_width="match_parent"
                android:layout_height="@dimen/cardHeight"
                android:layout_marginBottom="@dimen/cardBottomMargin"
                android:background="@color/cardBack"
                card_view:cardCornerRadius="@dimen/cardCornerRadius">

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:background="@color/cardBack"
                    android:orientation="vertical">

                    <ImageView
                        android:layout_width="match_parent"
                        android:layout_height="@dimen/imageHeight"
                        android:scaleType="centerCrop"
                        android:src="@drawable/picture_3"/>

                    <TextView
                        android:id="@+id/info_text3"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:layout_margin="@dimen/textMargin"
                        android:lineSpacingExtra="@dimen/spaceVertical"
                        android:textSize="@dimen/textSize"
                        android:text="@string/card_text_3" />
                </LinearLayout>
            </android.support.v7.widget.CardView>
        </LinearLayout>
    </ScrollView>
    <!-- ............................................... -->

</LinearLayout>
```
