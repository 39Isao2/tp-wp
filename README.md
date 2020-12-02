# tp_wp
tp_wpのwpテーマ化

1、Local by Flywheelに環境作る <br>
https://bazubu.com/local-by-flywheel-33920.html <br>
2、settingから日本語に<br>
3、style.cssを作成

```
/* style.css */
	
@charset "utf-8";

theme Name: tategami-portfolio
Author: tategami
Description: tategami-portfolioのWordPressテーマです。
version： 1.0.0

```
4、直下にstyle.cssを配置、topページをindex.phpに変更<br>
5、zipにしてアップ。テーマとして認識。<br>
6、直下にスクリーンショットを設置 (screenshot.png  880×660px)<br>

## まずはheader.phpの作成
7、index.phpのheader部分を編集してcssのパスを通す。<br>
8、header.phpの作成

#### もともと静的HTMLのheader部分
```
<!doctype html>
<html>
<head>
<meta charset="UTF-8">
<title>PLABE_Inc</title>
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="description" content="株式会社プレイブは「いいモノを、いい空間を」提供するデザイン会社です。">
<meta property="og:url" content="https://www.plabe.jp"/>
<meta property="og:title" content="TOP" />
<meta property="og:type" content="website">
<meta property="og:image" content="images/footer_logo.png"/>
<meta property="og:site_name" content="株式会社PLABE" />
<meta property="og:locale" content="ja_JP" />
<link rel="shortcut icon" href="images/logo_tate_white.png">
<link href="https://use.fontawesome.com/releases/v5.6.1/css/all.css" rel="stylesheet">
<link href="https://fonts.googleapis.com/css?family=Noto+Sans&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css?family=Open+Sans&display=swap" rel="stylesheet">
<link rel="stylesheet" href="css/reset.css">
<link rel="stylesheet" href="css/common.css">
<link rel="stylesheet" href="css/style.css">
</head>

<body>
	<header>
		<div class="navigation">
			<img src="images/header_mark_and_name.png" width="8%" alt="plabe_logo">
			<ul class="menu">
				<li class="menu_item"><a href="index.html">HOME</a></li>
				<li class="menu_item"><a href="about/index.html">ABOUT US</a></li>
				<li class="menu_item"><a href="company/index.html">COMPANY</a></li>
				<li class="menu_item"><a href="mailto:info@plabe.jp?subject=%8c%8f%96%bc&amp;body=%96%7b%95%b6">CONTACT</a></li>
			</ul>
			<div class="navigation_col">
				<a href="https://www.instagram.com/plabe_inc/?hl=ja" target="_blank"><i class="fab fa-instagram"></i></a>
				<a href="https://www.facebook.com/PLABEinc/" target="_blank"><i class="fab fa-facebook-f"></i></a>
				<a class="online-store-btn" href="https://theshop.plabe.jp/" target="_blank"><p>ONLINE STORE</p></a>
			</div>
		</div>
	</header>

```


#### wp化したheader部分 (ここまでをheader.phpにする)

このページで出てくるWPのタグ<br>
```

<!-- この2つはすごくよく使います！ -->

<!-- テーマのフォルダまでのパスを出力してくれます。-->
<?php echo get_template_directory_uri(); ?>

トップ/テーマの場所/
http://plabeinc.local/wp-content/themes/ を出力してくれる


<!-- トップページのURLを表示 -->
<?php echo home_url() ?>


<!-- 主にheadタグで使用 -->

<!-- ブログ名(サイト名)を表示 -->
<?php bloginfo('name'); ?> 

<!-- 現在のページ名を表示 -->
<?php wp_title(); ?>

<!-- ブログのdescriptionを表示 -->
<?php bloginfo( 'description' ); ?>

<!-- 直下のcss読み込む(テーマ名などの情報) -->
<?php bloginfo( 'stylesheet_url' ); ?>


```

### header.phpの完成

```

<!doctype html>
<html>
<head>
<meta charset="UTF-8">
<!-- ブログ名、各ページの記事やタイトル-->
<title><?php bloginfo('name'); ?> <?php wp_title(); ?></title>
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="description" content="<?php bloginfo( 'description' ); ?>">
<link rel="shortcut icon" href="<?php echo get_template_directory_uri(); ?>/images/logo_tate_white.png">
<!-- テーマのディレクトリ内のstyle.css読み込み -->
<link rel="stylesheet" href="<?php bloginfo( 'stylesheet_url' ); ?>">

<!-- ディスクリプションの設定 -->
<meta property="og:type" content="website">
<meta property="og:title" content="<?php the_title() ?>" />
<meta property="og:image" content="<?php echo get_template_directory_uri(); ?>/images/footer_logo.png"/>
<meta property="og:site_name" content="<?php bloginfo('name'); ?>" />

<!-- google フォント-->
<link href="https://use.fontawesome.com/releases/v5.6.1/css/all.css" rel="stylesheet">
<link href="https://fonts.googleapis.com/css?family=Noto+Sans&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css?family=Open+Sans&display=swap" rel="stylesheet">


<!-- css読み込み -->
<link rel="stylesheet" href="<?php echo get_template_directory_uri(); ?>/css/reset.css">
<link rel="stylesheet" href="<?php echo get_template_directory_uri(); ?>/css/common.css">
<link rel="stylesheet" href="<?php echo get_template_directory_uri(); ?>/css/style.css">

<!-- wpの様々な機能を使えるようにするタグ -->
<?php wp_head(); ?>

</head>

<!-- 各ページの情報のclassをつける(後に説明)-->
<body <?php body_class(); ?>>
	<header>
		<div class="navigation">
			<img src="<?php echo get_template_directory_uri(); ?>/images/header_mark_and_name.png" width="8%" alt="plabe_logo">
			<ul class="menu">
				<li class="menu_item"><a href="<?php echo home_url() ?>">HOME</a></li>
				<li class="menu_item"><a href="<?php echo home_url() ?>/about">ABOUT US</a></li>
				<li class="menu_item"><a href="<?php echo home_url() ?>/company">COMPANY</a></li>
				<li class="menu_item"><a href="<?php echo home_url() ?>/contact">COMPANY</a>CONTACT</a></li>
			</ul>
			<div class="navigation_col">
				<a href="https://www.instagram.com/plabe_inc/?hl=ja" target="_blank"><i class="fab fa-instagram"></i></a>
				<a href="https://www.facebook.com/PLABEinc/" target="_blank"><i class="fab fa-facebook-f"></i></a>
				<a class="online-store-btn" href="https://theshop.plabe.jp/" target="_blank"><p>ONLINE STORE</p></a>
			</div>
		</div>
	</header>

```

9、header.phpとして保存して、index.phpにインクルードする。

<img src="https://github.com/55Kaerukun/PLABE_INC_wp/blob/master/img/header.png" width="800px">

```
<!-- header.phpを読み込むタグ-->
<?php get_header(); ?>
```

### footer.phpの作成

```

<footer>
	<div class="footer_nav">
		<ul class="footer_menu">
			<li class="menu_item"><a href="<?php echo home_url() ?>/about">ABOUT US</a></li>
			<li class="menu_item"><a href="<?php echo home_url() ?>/company"></li>
			<li class="menu_item"><a href="mailto:info@plabe.jp?subject=%8c%8f%96%bc&amp;body=%96%7b%95%b6">CONTACT</a></li>
			<li class="menu_item"><a href="<?php echo home_url() ?>/policy">PRIVACY POLICY</a></li>
		</ul>
		<a href="index.html"><img src="<?php echo get_template_directory_uri(); ?>/images/footer_logo.png" alt="footer_logo"></a>
		<p>© 2020 PLABE Inc. All rights reserved.</p>
	</div>
</footer>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/2.0.1/TweenMax.min.js"></script>
<script src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/85188/jquery.wavify.js"></script>
<script>
	$(function(){
// 設定
var $width ='100%'; // 横幅
var $height =1000; // 高さ
var $interval = 3000; // 切り替わりの間隔（ミリ秒）
var $fade_speed = 2000; // フェード処理の早さ（ミリ秒）
$("#slide ul li").css({"position":"relative","overflow":"hidden","width":$width,"height":$height});
$("#slide ul li").hide().css({"position":"absolute","top":0,"left":0});
$("#slide ul li:first").addClass("active").show();
setInterval(function(){
var $active = $("#slide ul li.active");
var $next = $active.next("li").length?$active.next("li"):$("#slide ul li:first");
$active.fadeOut($fade_speed).removeClass("active");
$next.fadeIn($fade_speed).addClass("active");
},$interval);
});
	
//	$(function() {
//	setTimeout(function(){
//		$('.start p').fadeIn(2000);
//	},800); //0.5秒後にロゴをフェードイン!
//	setTimeout(function(){
//		$('.start').fadeOut(1500);
//	},3000); //2.5秒後にロゴ含め真っ白背景をフェードアウト！
//});
	</script>
	
<!-- wpの色々な機能を使えるようにする -->
<?php wp_footer(); ?>
</body>
</html>

```

10、footer.phpとして保存して、index.phpにインクルードする。

<img src="https://github.com/55Kaerukun/PLABE_INC_wp/blob/master/img/footer.png" width="600px">


11、index.phpの仕上げで他の部分も各所、WPのタグに書き換えましょう<br>
```
<!-- これしか使いません。-->
<?php echo get_template_directory_uri(); ?>

<?php echo home_url() ?>

```
index.phpのソース<br>
https://gist.github.com/55Kaerukun/585068d5c4c371af4d7cbd2882bf8570

### 管理画面から固定ページ制作の準備
WPでは、下層ページのことを（固定ページ）と呼びます。<br>

<img src="https://github.com/55Kaerukun/PLABE_INC_wp/blob/master/img/kanri.png" width="600px">

12、パーマリンク設定(URLのルールを設定します)

<img src="https://github.com/55Kaerukun/PLABE_INC_wp/blob/master/img/permalink.png" alt="600px">

```
カスタム構造 : /%category%/%postname%
```
参考 : https://liginc.co.jp/web/wp/customize/148458

現状このような感じなので、下層ページを固定ページにしていきましょう！


<img src="https://github.com/55Kaerukun/PLABE_INC_wp/blob/master/img/directory.png" width="600px">

13、下層ページ(固定ページ)テンプレートの作成

### page.php
```

<!-- header.phpの読み込み -->
<?php get_header(); ?>
 
  <!-- 固定ページのタイトルが表示されます。 -->
  <h1><?php the_title(); ?></h1>

  
  <!-- 投稿があるかifで判断してあったら表示する、wpのおまじない的な書き方-->
  <?php if(have_posts()): while(have_posts()):the_post(); ?>
  
  	<!-- 固定ページのエディタ内の内容表示 -->
  	<?php the_content(); ?>
  
  <?php endwhile; endif; ?>

 
<!-- footer.phpの読み込み -->
<?php get_footer(); ?>

```

14、固定ページに書き写しましょう。（画像URLの置き換えがちょっと大変）

```
ここも一括置換

// 画像までのパス
http://plabeinc.local/wp-content/themes/PLABE_INC/images/
```


<img src="https://github.com/55Kaerukun/PLABE_INC_wp/blob/master/img/page.png" width="600px">



### 条件分岐タグの使い方header.phpのcssの読み込み変更
```


<?php if ( 条件 ) : ?>
条件を満たした内容が表示される
<?php endif; ?>


<!-- もしトップページだったら -->
<?php if (  is_front_page() ||  is_home() ) : ?>
<link rel="stylesheet" href="<?php echo get_template_directory_uri(); ?>/css/style.css">
<?php endif; ?>

<!-- もし固定ページでスラッグaboutだったら -->
<?php if ( is_page('about') ) : ?>
<link rel="stylesheet" href="<?php echo get_template_directory_uri(); ?>/css/about.css">
<?php endif; ?>


↑ companyもpolicyも同じように書いてあげましょう。


参考: WPよく使う条件分岐タグ
https://webdesignday.jp/inspiration/wordpress/4765/#is_page

```

1日目ノルマ終了。

<br>

追加css <br>
https://gist.github.com/55Kaerukun/020df64ca00164727b1af762ec59d104

```

bodyタグの変更 (ページの情報をクラス名として出力してくれる命令)
<body <?php body_class(); ?>>
```

15、個別記事のファイルを作りましょう。
### single.php


```


<!-- ヘッダー読み込み -->
<?php get_header(); ?>

<main>

	<!-- 記事があったら表示 -->
	<?php if(have_posts()): while(have_posts()):the_post(); ?>
	  
	
	  	<!-- 投稿タイトルを表示 -->
	  	<h2><?php the_title(); ?></h2>


	  	<!-- 投稿日時を表示 -->
	  	<time><?php the_time('Y.m.d'); ?></time>

	  	<!-- 投稿カテゴリーを表示 -->
	  	<p><?php the_category(); ?></p>
	  
	
		<!-- エディタで入力したコンテンツ部分を表示 -->
	    <div>
	    	<?php the_content(); ?>
	    </div>
	  
	<?php endwhile; endif; ?>

	  
	<!-- ページャーの表示 -->
	<div class="pager">
		<?php previous_post_link('%link','前の記事へ'); ?>
		<?php next_post_link('%link','次の記事へ'); ?>
	</div>

</main>


<!-- フッター読み込み -->
<?php get_footer(); ?>



```

16、投稿→カテゴリーから、カテゴリーを作成しておく。<br>

<img src="https://github.com/55Kaerukun/PLABE_INC_wp/blob/master/img/cat.png" width="800px">

17、記事を投稿しましょう。<br>

### 投稿画面
<img src="https://github.com/55Kaerukun/PLABE_INC_wp/blob/master/img/toukou.png" width="800px">
<br>
<br>
<img src="https://github.com/55Kaerukun/PLABE_INC_wp/blob/master/img/toukouKekka.png" width="800px">
<br>
<br>


<img src="https://github.com/55Kaerukun/PLABE_INC_wp/blob/master/img/news.png" width="800px">





### 投稿部分のphp化

```

<!-- news部分 -->
<section class="news_section">
	<h2>News & Topics</h2>
	<ul>
		<li><a href="#"><span>2020.10.1</span>ホームページがリニューアルしました。</a></li>
		<li><a href="#"><span>2020.10.1</span>臨時休業のお知らせ</a></li>
		<li><a href="#"><span>2020.10.1</span>新商品追加のお知らせ</a></li>
	</ul>
</section>
	
```

### WordPressループ
```

<!-- 投稿が存在したらその表示-->
<?php if (have_posts()) : ?>
	<?php while (have_posts()) : the_post(); ?>

    <!-- 投稿日時 -->
    <?php the_time('Y年m月d日') ?>

    <!-- 投稿のリンク先 -->
    <a href="<?php the_permalink() ?>">
        <!-- 投稿タイトル -->
        <?php the_title(); ?>
    </a>
	
<?php endwhile; ?>
<?php else : ?>
    <p>投稿が見つかりませんでした。</p>
<?php endif; ?>


```



トップページnews部分のphp化（今回用にループに組み込む）
```
<!-- news部分のphp化 -->
<section class="news_section">
	<h2>News & Topics</h2>
	<ul>
	  <?php
	    $args = array(
	      'posts_per_page' => 3 // 表示件数の指定
	    );
	    $posts = get_posts( $args );
	    
	    foreach ( $posts as $post ): // ループの開始
	    setup_postdata( $post ); // 記事データの取得
	  ?>
	  
	    <li><a href="<?php the_permalink() ?>"><span><?php the_time('Y年m月d日') ?></span><?php the_title(); ?></a></li>
	    
	<?php
	  endforeach; // ループの終了
	  wp_reset_postdata();
	?>
	</ul>
</section>


```





18、記事一覧ページの作成<br>

function.phpに記述してサムネイルを使用できるようにする。

### functions.php
https://designsupply-web.com/media/knowledgeside/1815/
```
<?php

// アイキャッチを使用可能に
add_theme_support('post-thumbnails');
add_image_size( 'custom_thumbnails', 300, 300, true );


```


参考 : ページの優先順位 <br>
https://plusers.net/wordpress_theme_8 <br>


### category.phpの作成


<img src="https://github.com/55Kaerukun/PLABE_INC_wp/blob/master/img/catlist.png" width="800px">

```

<?php get_header(); ?>

<main>
  
<p><?php single_cat_title(); ?> カテゴリー記事の一覧です</p>

<?php if(have_posts()): while(have_posts()):the_post(); ?>

  <div class="content">
    <!-- 投稿日付 -->
    <time><?php the_time('Y.m.d'); ?></time>

    <!-- タイトル出力 -->
    <h2><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h2>

    <!-- アイキャッチ出力 -->
    <?php the_post_thumbnail('thumbnail'); ?>
    
<?php get_header(); ?>

<main>
  
<p><?php single_cat_title(); ?> カテゴリー記事の一覧です</p>

<section class="contents">

<?php if(have_posts()): while(have_posts()):the_post(); ?>



  <div class="content">
    
    <!-- 投稿日付 -->
    <time><?php the_time('Y.m.d'); ?></time>

    <!-- タイトル出力 -->
    <h2><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h2>

    
    <a href="<?php the_permalink(); ?>">

<?php
if (has_post_thumbnail()) {
	the_post_thumbnail( array(300,300) );
} else {
	 echo '<img src="http://plable2.local/wp-content/themes/plable/images/default.png">';
}
?>

    </a>

  </div>
  
<?php endwhile; endif; ?>

</section>
  
<div class="pager">
    <?php previous_posts_link('次のページへ'); ?>
    <?php next_posts_link('前のページへ'); ?>
</div>
</main>

<?php get_footer(); ?>


  </div>
  
<?php endwhile; endif; ?>
  
<div class="pager">
    <?php previous_posts_link('次のページへ'); ?>
    <?php next_posts_link('前のページへ'); ?>
</div>
</main>

<?php get_footer(); ?>

```

flex版 <br>
https://gist.github.com/55Kaerukun/9967a7030c72c5a16d82f03982a96067

### お問い合わせフォームの作成（ Contact Form 7）
一番有名なお問い合わせフォーム作成プラグイン

<img src="http://hareumi.com/githubWP/ContactForm7.jpg" width="500px">

プラグイン → 新規追加 プラグインを検索 → Contact Form 7 → インストール → いますぐ有効化

<img src="http://hareumi.com/githubWP/cf7.jpg" width="400px">

ショートコードをコピー 

<img src="http://hareumi.com/githubWP/cf7_2.jpg" width="800px">

固定ページを作って貼り付け → 更新

<img src="http://hareumi.com/githubWP/cf7_3.jpg" width="400px">

フォーム完成！


### 本番アップ作業

0、本番サーバーにWordPressをインストールしておく。

1、プラグイン「All in one Migration」を使って本番サーバーに引っ越す。
https://webst8.com/blog/wordpress-all-in-one-migration/  <br><br>

2、プラグイン「Search Regex」を使って、画像やパスなどのURLを一括変換 <br><br>
https://favorite-fashion.com/blog043/



#### その他
カスタム投稿タイプの作り方(投稿の種類を増やせます、そこそこ使うかも)<br>
https://webst8.com/blog/wordpress-custom-posts/


```

/* カスタム投稿 */
// 経営資産速報
function create_post_type3() {
  $exampleSupports3 = [
    'title',
    'editor',
    'thumbnail',
    'revisions'
  ];

  // add post type
  register_post_type( 'management_news',
    array(
      'label' => '資産形成NEWS',
      'public' => true,
      'has_archive' => true,
      'menu_position' => 5,
      'supports' => $exampleSupports3
    )
  );

  // add taxonomy
  register_taxonomy(
    'management_news_category',
    'management_news',
    array(
      'label' => 'カテゴリー',
      'labels' => array(
        'all_items' => 'カテゴリー一覧',
        'add_new_item' => '新規カテゴリーを追加'
      ),
      'hierarchical' => true
    )
  );
}

add_action( 'init', 'create_post_type3' );




```
<br>
プラグイン「Advanced Custom Fieldsの使い方」<br>
http://galileo-venus.com/2020/05/14/20200507_wp_acf01/
<br>
プラグイン「All in one SEOパック」より細かくページごとのSEOの設定ができるプラグインです。
https://bazubu.com/all-in-one-seo-pack-23836.html
<br>

