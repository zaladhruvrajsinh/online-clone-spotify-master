# Spotify Clone

## Introduction

In this session we will clone the [Spotify](https://www.spotify.com/us/) landing page. We'll use the concepts of HTML and CSS we've explained in the previous session with the [Netflix clone](https://github.com/assimovt/ironhack-netflix-clone) and build upon that. Therefore, if you haven't followed it along, please do so now.

The overall site is pretty similar to Netflix. It also has the navigation in the top, several main sections, and the footer. Additionally, it has some effects with JavaScript, such as carousel, which we will skim through - remember we're mostly focused on learning HTML/CSS and JavaScript is beyond the scope of this material.

## Basic structure

In the last session, we've built everything from scratch with CSS. However, because it's so common to create grids, buttons, dropdowns, and other components in CSS and JavaScript, folks from various companies have outsourced their code and created so called HTML/CSS/JS frameworks.

Perhaps the most known and used one is the Twitter's [Bootstrap](http://getbootstrap.com) framework and that's what we gonna use in this session.

So, let's create a basic HTML structure with Bootstrap and their provided [CSS/JS](http://getbootstrap.com/getting-started/#download):

    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title>Spotify</title>

        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
      </head>

      <body>
        <h1>Hello Bootstrap</h1>

        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
        <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>
      </body>
    </html>

Notice how we've added the new `<meta>` property named _viewport_. This is required for building responsive websites. It instructs browser to adjust the page width to the screen (desktop, phone, etc.) and to start with an initial zoom of 1.

## Adding navigation bar

From now on, whenever adding a new component to the page, we'll be following the layout outlined by Twitter Bootstrap framework. For instance, to add a [navbar](http://getbootstrap.com/components/#navbar) in a Bootstrap fashion:

    <header class="navbar navbar-dark navbar-fixed-top" role="banner">
      <div class="container">
        <div class="navbar-header">
          <a href="#">
            <span class="navbar-logo">Spotify</span>
          </a>
        </div>

        <nav class="collapse navbar-collapse" id="navbar-nav" role="navigation">
          <ul class="nav navbar-nav navbar-right nav-main">
            <li class="hidden">
              <a href="#" id="nav-link-Explore">
                Explore
              </a>
            </li>
            <li>
              <a href="#" id="nav-link-premium">
                Premium
              </a>
            </li>
            <li>
              <a href="#" id="nav-link-help">
                Help
              </a>
            </li>
            <li>
              <a href="#" id="nav-link-download">
                Download
              </a>
            </li>
            <li role="separator" class="divider"></li>
            <li>
              <a href="#" id="nav-link-sign-up">
                Sign up
              </a>
            </li>
            <li>
              <a href="#" id="header-login-link">
                Log In
              </a>
            </li>
          </ul>
        </nav>
      </div>
    </header>

Notice how the CSS we linked styled the navigation bar and added the default mouse over and other effects. But that's default Bootstrap styles, let's customize them now with our own CSS. As previously, create a `css` folder with `style.css` and link it to the page:

    <link rel="stylesheet" href="css/style.css"/>

Now, let's add the logo in _SVG_ format to `img` folder. Finally, add the corresponding CSS:

    body {
      font-family: Helvetica,Arial,sans-serif;
      font-size: 16px;
      line-height: 1.5;
      color: #222326;
    }

    .navbar-dark {
      background-color: rgba(0,0,0,.6);
    }

    .navbar-dark .navbar-nav>li>a {
      color: #fff;
      padding: 28px 17px;
      font-weight: 700;
      line-height: 24px;
    }

    .nav>li>a:focus,
    .nav>li>a:hover {
      background-color: inherit;
      color: #9bf0e1;
    }

    .nav .divider {
      background-color: #d9dadc;
      width: 1px;
      height: 16px;
      margin: 32px 17px;
    }

    .navbar-logo {
      margin-top: 20px;
      margin-bottom: 20px;
      width: 132px;
      height: 40px;
      background-repeat: no-repeat;
      background-size: 100% 100%;
      font: 0/0 a;
      color: transparent;
      text-shadow: none;
      background-color: transparent;
      border: 0;
      float: left;
      background-image: url('../img/logo.svg');
    }


## Adding main background

Let's add the main background above the `header` section.

HTML:

    <div class="bg-main">
      <div class="bg-main-img"></div>
    </div>

CSS:

    .bg-main {
      width: 100%;
      height: 100%;
      background: linear-gradient(50deg, #ff4169 0, #7c26f8 100%);
      position: fixed;
      left: 0;
      top: 0;
      z-index: -1;
    }

    .bg-main-img {
      display: block;
      background-image: url('../img/bg-albums.png');
      width: 100%;
      height: 100%;
      background-position: center;
    }

## Adding carousel

To add the carousel slider we will use two Bootstrap components. First is so called [jumbotron](http://getbootstrap.com/components/#jumbotron), which is used to call the extra attention to the content by placing it in the middle and to extend to the entire viewport.

Then, inside `jumbotron`, we will add the [Bootstrap carousel](http://getbootstrap.com/javascript/#carousel), which uses JavaScript to create beautiful, responsive slider.

So, let's get to HTML part first:

    <div class="jumbotron">
      <div class="container">
        <div id="carousel-tour" class="carousel slide" data-ride="carousel" data-interval="false">

          <!-- Indicators -->
          <ol class="carousel-indicators">
            <li data-target="#carousel-tour" data-slide-to="0" class="active js-button-hero-carousel-dots"></li>
            <li data-target="#carousel-tour" data-slide-to="1" class="js-button-hero-carousel-dots"></li>
            <li data-target="#carousel-tour" data-slide-to="2" class="js-button-hero-carousel-dots"></li>
            <li data-target="#carousel-tour" data-slide-to="3" class="js-button-hero-carousel-dots"></li>
          </ol>

          <!-- Wrapper for slides -->
          <div class="carousel-inner" role="listbox" style="height: 307px;">
            <div class="item active">
              <h1>
                <span class="text-white">
                  3 months of Premium for $0.99.
                </span>
              </h1>
              <a href="#" class="btn btn-lg btn-solid js-button-hero-get-premium">
                Learn More
              </a>
              <p class="text-center text-white text-signup">
                Or sign up for our <a href="#" class="js-goto-signup">free service</a>.
              </p>
            </div>

            <div class="item">
              <h1>
                <span class="text-white">
                  Premium for your whole family.<br>Just $14.99.
                </span>
              </h1>
              <a href="#" class="btn btn-solid js-button-hero-family">
                LEARN MORE
              </a>
            </div>

            <div class="item">
              <h1>
                <span class="text-white">
                  Students get 50% off Premium.
                </span>
              </h1>
              <a href="#" class="btn btn-solid js-button-hero-student">
                LEARN MORE
              </a>
            </div>

            <div class="item">
              <h1>
                <span class="text-white">
                  Play Spotify on PlayStation®.
                </span>
              </h1>
              <a href="#" class="btn btn-solid js-button-hero-playstation">
                LEARN MORE
              </a>
            </div>
          </div>

          <!-- Controls -->
          <a class="left carousel-control js-button-hero-carousel-left-arrow" href="#carousel-tour" data-slide="prev">
            <span class="icon-prev"></span>
            <span class="sr-only">
              Previous
            </span>
          </a>
          <a class="right carousel-control js-button-hero-carousel-right-arrow" href="#carousel-tour" data-slide="next">
            <span class="icon-next"></span>
            <span class="sr-only">
              Next
            </span>
          </a>
        </div>
      </div>
    </div>

And then applying CSS:

    .text-white {
      color: white;
    }

    .jumbotron {
      background: none;
      padding: 100px 0;
      text-align: center;
      margin: 0;
    }

    .carousel-control.right, .carousel-control.left {
      background: none;
    }

    .btn {
      padding: 17px 48px;
      font-size: 14px;
      line-height: 1;
      border-radius: 500px;
      padding: 18px 48px 16px;
      transition-property: background-color,border-color,color,box-shadow,filter;
      transition-duration: .3s;
      border-width: 0;
      letter-spacing: 2px;
      min-width: 160px;
      text-transform: uppercase;
      white-space: normal;
    }

    .jumbotron .btn {
      margin: 20px 10px 30px;
    }

    .btn-solid {
      color: #fff;
      background-color: #7c25f8;
    }
    .btn-solid:hover {
      color: #fff;
      background-color: #6207e3;
    }

    .btn-lg {
      font-size: 16px;
      line-height: 1;
      border-radius: 500px;
      padding: 21px 56px 19px;
    }

    .item h1 {
      font-weight: 900;
    }

    .text-signup a {
      color: #fff;
      text-decoration: underline;
    }

    #carousel-tour {
      margin-top: 50px;
    }

Notice how we've added `transition-property` and `transition-duration` to the `.btn` class. This specifies the properties to apply transition effect, in this case `background-color,border-color,color,box-shadow,filter` and for how long it will last, which is 0.3 second in our case.

## Adding custom fonts

What you'd notice is we don't have the same fonts that Spotify has. For that, we'll add their `circular-medium.woff2` font to our `css` directory and use the CSS `@font-face` rule to define our custom font:

    @font-face {
      font-family: Circular;
      src: url('circular-medium.woff2');
    }

    ...
    body {
      font-family: Circular,Helvetica,Arial,sans-serif;
      ...
    }

## Adding "What's on Spotify"

Now, let's move on to "What's on Spotify" section.

HTML:

    <div class="container">
      <a class="btn-scroll" name="whats-on-spotify" href="#whats-on-spotify">
        <span class="btn-scroll-text">LEARN ABOUT SPOTIFY</span>
      </a>
    </div>

    <div class="jumbotron jumbotron-whats-on bg-white">
      <div class="container">
        <div class="row">
          <div class="col-sm-7 col-sm-push-5 col-md-5 col-md-push-7">
            <h2 class="text-klein-purple">
              What’s on Spotify?
            </h2>
            <div>
              <h3 class="text-klein-purple">
                Music
              </h3>
              <p>
                There are millions of songs on Spotify. Play your favorites, discover new tracks, and build the perfect collection.
              </p>
            </div>
            <div>
              <h3 class="text-klein-purple">
                Playlists
              </h3>
              <p>
                You’ll find readymade playlists to match your mood, put together by music fans and experts.
              </p>
            </div>
            <div>
              <h3 class="text-klein-purple">
                New Releases
              </h3>
              <p>
                Hear this week’s latest singles and albums, and check out what’s hot in the Top 50.
              </p>
            </div>
          </div>

          <div class="col-sm-5 col-sm-pull-7 col-md-6 col-md-pull-5">
            <div class="albums row">
              <img src="https://i.scdn.co/image/6c41981dc659cc8a19a0371f42951d8dec48db7c"
                   class="album-img col-sm-6"/>
              <img src="https://i.scdn.co/image/24a63c5c743b4376b7b7d570cf4a83ea017382fd"
                   class="album-img col-sm-6"/>
              <img src="https://i.scdn.co/image/017f05aea238929a9b3970743a879c90bfff23ca"
                   class="album-img col-sm-6"/>
              <img src="https://i.scdn.co/image/62cbbb3ffd4dd111c11e8f0d2ac0c5dfa1585a1f"
                   class="album-img col-sm-6"/>
            </div>
          </div>
        </div>
      </div>
    </div>

And the corresponding CSS:

    ...

    .text-klein-purple {
      color: #7c25f8;
    }
    ...
    .bg-white {
      background-color: #fff;
    }
    ...
    a.btn-scroll {
      text-decoration: none;
      color: white;
      display: block;
      text-align: center;
    }

    a.btn-scroll:hover {
      color: #9bf0e1;
    }

    .btn-scroll-text {
      text-transform: uppercase;
      transition: color .3s ease-in-out;
      display: block;
      font-weight: 700;
      letter-spacing: .1em;
      margin-bottom: 20px;
    }

    h2 {
      font-size: 50px;
      line-height: 1;
      margin: 0 0 .75em;
      font-weight: 900;
    }

    h3 {
      font-size: 40px;
      font-weight: 900;
      line-height: 1.4;
    }

    .jumbotron-whats-on {
      text-align: left;
      padding: 180px 0;
    }

    .jumbotron p {
      font-weight: 400;
      font-size: 18px;
      margin: 1em 0;
    }

    .album-img {
      padding: 0;
    }

## Adding benefits with phone images

The next section are the benefits of the app with some cool phone images. First, HTML:

    <div class="jumbotron">
      <div class="container">
        <div class="row">
          <div class="col-sm-4 text-left text-white">
            <div>
              <h2>
                It's easy.
              </h2>
            </div>
            <div>
              <h3 class="text-aquamarine">
                Search
              </h3>
              <p>
                Know what you want to listen to? Just search and hit play.
              </p>
            </div>
            <div>
              <h3 class="text-aquamarine">
                Browse
              </h3>
              <p>
                Check out the latest charts, brand new releases and great playlists for right now.
              </p>
            </div>
            <div>
              <h3 class="text-aquamarine">
                Discover
              </h3>
              <p>
                Enjoy new music every Monday with your own personal playlist. Or sit back and enjoy Radio.
              </p>
            </div>
          </div>

          <div class="devices-container">
            <div class="row">
              <div class="col-xs-4">
                <div class="iphone iphone-1">
                  <img src="https://d2c87l0yth4zbw-2.global.ssl.fastly.net/i/home/iphone-1a.jpg">
                </div>
              </div>
              <div class="col-xs-4">
                <div class="iphone iphone-2">
                  <img src="https://d2c87l0yth4zbw.global.ssl.fastly.net/i/home/iphone-2.jpg">
                </div>
                <div class="iphone iphone-3">
                  <img src="https://d2c87l0yth4zbw-2.global.ssl.fastly.net/i/home/iphone-3.jpg">
                </div>
              </div>
              <div class="col-xs-4">
                <div class="iphone iphone-4">
                  <img src="https://d2c87l0yth4zbw-2.global.ssl.fastly.net/i/home/iphone-4.jpg">
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

And CSS:

    .text-aquamarine {
      color: #9bf0e1;
    }
    ...
    .iphone {
      width: 358px;
      height: 730px;
      padding: 80px 22px 0;
      margin-bottom: 30px;
      background: url('../img/iphone-klein-purple.png') no-repeat;
      background-size: cover;
    }

    .iphone-1, .iphone-4 {
      margin-top: 200px;
    }

    .devices-container {
      margin-top: -350px;
      margin-bottom: -620px;
      margin-right: -100%;
      float: left;
      transform: rotate(30deg) translate3d(0,40px,0);
    }

    .devices-container img {
      max-width: 100%;
    }

As earlier, we've used the CSS `transform` property, but now a shorter form where we can put a number of transformation properties in a single line. Here, we `rotate` by 30 degrees and also use CSS 3D transformation to move the images by 40px on y-axis.

## Adding support devices section

Next up, supported devices section. HTML:

    <div class="jumbotron jumbotron-devices">
      <div class="container">
        <img class="center-block" src="https://d2c87l0yth4zbw.global.ssl.fastly.net/i/home/all-devices.svg">
        <div>
          <h2>
            <span class="text-white">
              One account. Listen everywhere.
            </span>
          </h2>
        </div>
        <ul class="device-list text-white">
          <li>Mobile</li>
          <li>Computer</li>
          <li>Tablet</li>
          <li>Car</li>
        </ul>
        <ul class="device-list text-white">
          <li>Speaker</li>
          <li><a href="#">PlayStation®</a></li>
          <li>TV</li>
          <li><a href="#">Web Player</a></li>
        </ul>
      </div>
    </div>

CSS:

    .jumbotron-devices {
      background: #222326;
    }

    .jumbotron-devices img {
      margin-bottom: 60px;
    }

    .jumbotron-devices .device-list {
      display: inline;
      padding-left: 0;
      list-style: none;
      margin-left: -5px;
      text-transform: uppercase;
      font-weight: 700;
    }

    .jumbotron-devices .device-list li {
      display: inline-block;
      padding-left: 5px;
      padding-right: 5px;
      margin: 1em 0;
    }

    .jumbotron-devices .device-list li:after {
      content: '-';
      padding-left: 14px;
      color: #7c25f8;
    }

    .jumbotron-devices .device-list li:last-child:after {
      content: '';
    }

    .jumbotron-devices .device-list a {
      color: white;
      border-bottom: 1px solid white;
      text-decoration: none;
    }

And to fix the overlapping of the previous section, we could add:

    .jumbotron {
      ...
      position: relative;
    }

## Adding subscriptions section

This one is pretty straightforward:

    <div class="jumbotron jumbotron-subscriptions">
      <div class="container">
        <div class="row">
          <div class="col-md-10">
            <div class="row">
              <div class="col-sm-10 col-lg-8">
                <div>
                  <h1>
                    <span class="text-white">
                      Go get the music.
                    </span>
                  </h1>
                </div>
                <div>
                  <p class="text-white">
                    Listen free.
                    <br>
                    Or go Premium to play on-demand, anywhere.
                  </p>
                </div>
              </div>
            </div>
            <div class="row">
              <div class="col-sm-10">
                <div>
                  <h3 class="price-title text-aquamarine">Spotify</h3>
                  <h3 class="price text-white">
                    $0.00 <span class="month text-aquamarine"> / month</span>
                  </h3>
                  <div class="clearfix"></div>
                  <ul class="details-subscriptions text-white">
                    <li>
                      Enjoy your favorite albums and artists, with occasional ads.
                    </li>
                  </ul>
                  <a href="#" class="btn btn-solid">
                    GET SPOTIFY FREE
                  </a>
                </div>

                <div class="clearfix"></div>


                <div class="animated animatedFadeInUp fadeInUp">
                  <h3 class="price-title text-aquamarine">
                    Spotify Premium
                  </h3>
                  <h3 class="price text-white">
                    $0.99 <span class="month text-aquamarine"> /3 months</span>
                  </h3>
                  <div class="clearfix"></div>
                  <div class="tour-variation">
                    <p class="h3-sub text-white"><a href="/us/family/" data-ga-category="home (subscriptions)" data-ga-action="family">Family</a> and <a href="/us/student/" data-ga-category="home (subscriptions)" data-ga-action="student">Student</a> offers available</p>

                    <p class="h3-sub text-white">Only $9.99/month after.</p>
                  </div>
                  <div class="clearfix"></div>

                  <ul class="details-subscriptions text-white">
                    <li>
                      Play on-demand.
                    </li>
                    <li>
                      Listen offline.
                    </li>
                    <li>
                      No ads.
                    </li>
                    <li>
                      High quality audio.
                    </li>
                  </ul>
                  <a href="#" class="btn btn-solid">
                    GET SPOTIFY PREMIUM
                  </a>
                </div>
              </div>
            </div>
          </div>
          <div class="grid-overflow hidden-xs hidden-sm">
            <div class="animated animatedFadeInUp fadeInUp">
              <div class="nexus">
                <img src="https://d2c87l0yth4zbw.global.ssl.fastly.net/i/home/android-1.jpg" style="display: block;">
              </div>
            </div>
          </div>
        </div>
        <p class="text-center legal text-white">
          Only $9.99/month after. Offer not available to users who already tried Premium. <a class="text-aquamarine" href="#">Terms apply.</a>
        </p>
      </div>
    </div>

As you noticed, we've used `.grid-overflow` class, which we will use to extract the image positioning functionality we used in devices section:

    .devices-container {
      margin-top: -350px;
      margin-bottom: -620px;
      transform: rotate(30deg) translate3d(0,40px,0);
    }

    .grid-overflow {
      margin-right: -100%;
      float: left;
    }

And finally add the `grid-overflow` class to `devices-container`:

    <div class="grid-overflow devices-container">

We're all set to put the last bits of CSS for this section:

    .jumbotron h1 {
      font-weight: 900;
    }
    ...


    .jumbotron-subscriptions {
      padding: 150px 0 0;
      text-align: left;
    }

    .jumbotron-subscriptions .btn {
      margin-top: 30px;
      margin-bottom: 70px;
    }

    .price-title {
      float: left;
      margin: 0;
    }

    .price {
      float: right;
      margin: 0 0 12px;
    }

    .month {
      font-size: 20px;
    }

    .details-subscriptions {
      border: 1px solid white;
      border-left: 0;
      border-right: 0;
      padding: 16px 0;
      padding-left: 0;
      list-style: none;
      font-weight: 700;
      margin-bottom: 0;
    }

    .details-subscriptions {
      font-size: 24px;
    }

    .tour-variation p:first-child {
      float: left;
    }

    .tour-variation p:last-child {
      float: right;
    }

    .tour-variation a {
      color: #9bf0e1;
      text-decoration: none;
    }

    .tour-variation a:hover {
      color: #42e3c6;
    }

    p.legal {
      font-size: 12px;
      margin-top: 8px;
    }

    p.legal a {
      text-decoration: underline;
    }

    p.legal a:hover {
      color: #42e3c6;
    }

    .nexus {
      width: 458px;
      height: 873px;
      padding: 60px 24px 0 18px;
      background: url('../img/nexus-klein-purple.png') no-repeat;
      background-size: cover;
      margin-bottom: -50%;
    }

    .nexus img {
      max-width: 100%;
    }

## Adding footer

The last bit of this page is the footer section.

      <footer role="contentinfo" class="footer footer-highlight-aquamarine">
        <div class="container">
          <nav class="row">
    
            <div class="col-xs-12 col-md-2">
              <div class="footer-logo">
                <a href="#">Spotify</a>
              </div>
            </div>
    
            <div class="col-xs-6 col-sm-4 col-md-2">
              <h3 class="nav-title">Company</h3>
              <ul class="nav">
    
                <li>
                  <a href="#" id="nav-link-about">
                    About
                  </a>
                </li>
    
                <li>
                  <a href="#" id="nav-link-jobs">
                    Jobs
                  </a>
                </li>
    
                <li>
                  <a href="#" id="nav-link-press">
                    Press
                  </a>
                </li>
    
                <li>
                  <a href="#" id="nav-link-news">
                    News
                  </a>
                </li>
    
              </ul>
            </div>
    
            <div class="col-xs-6 col-sm-4 col-md-2">
              <h3 class="nav-title">Communities</h3>
              <ul class="nav">
    
                <li>
                  <a href="#" id="nav-link-artists">
                    For Artists
                  </a>
                </li>
    
                <li>
                  <a href="#" id="nav-link-developers">
                    Developers
                  </a>
                </li>
    
                <li>
                  <a href="#" id="nav-link-brands">
                    Brands
                  </a>
                </li>
    
              </ul>
            </div>
    
            <div class="col-xs-6 col-sm-4 col-md-2">
              <h3 class="nav-title">Useful links</h3>
              <ul class="nav">
                <li>
                  <a href="#" id="nav-link-help">
                    Help
                  </a>
                </li>
    
                <li>
                  <a href="#" id="nav-link-gift">
                    Gift
                  </a>
                </li>
    
                <li class="hidden-xs ">
                  <a href="#" id="nav-link-play">
                    Web Player
                  </a>
                </li>
    
              </ul>
            </div>
    
            <div class="col-xs-12 col-md-4 col-social">
              <ul class="nav">
                <li>
                  <a href="#">
                    <img alt="instagram" src="img/instagram-icon.svg"/>
                  </a>
                </li>
                <li>
                  <a href="#">
                    <img alt="twitter" src="img/twitter-icon.svg"/>
                  </a>
                </li>
                <li>
                  <a href="#">
                    <img alt="facebook" src="img/facebook-icon.svg"/>
                  </a>
                </li>
              </ul>
            </div>
          </nav>
    
          <nav class="row row-small">
            <div class="col-xs-8 col-md-6">
    
              <ul class="nav nav-small">
                <li>
                  <a href="#">Legal</a>
                </li>
                <li>
                  <a href="#">Privacy</a>
                </li>
                <li>
                  <a href="#">Cookies</a>
                </li>
                <li>
                  <a href="#">About Ads</a>
                </li>
              </ul>
            </div>
    
            <div class="col-xs-4 col-md-6 text-right">
              <a class="market" href="#" title="Click to change">
                <div class="media">
                  <div class="media-body media-middle">
                    USA
                  </div>
                  <div class="media-right media-middle">
                    <span class="media-object flag-icon flag-icon-us"></span>
                  </div>
                </div>
              </a>
    
              <small class="copyright">&copy; 2017 Spotify AB</small>
            </div>
          </nav>
        </div>
      </footer>

And the CSS:

    .footer {
      background-color: black;
      color: white;
      padding: 80px 0 50px;
      text-align: left;
    }

    .footer-highlight-aquamarine a {
      color: white;
    }

    .footer-highlight-aquamarine a:hover {
      color: #9bf0e1;
    }

    .footer-logo a {
      display: block;
      width: 132px;
      height: 40px;
      font: 0/0 a;
      color: transparent;
      border: 0;
      background-image: url('../img/logo.svg');
      background-repeat: no-repeat;
      background-size: 100% 100%;
      margin-bottom: 50px;
    }

    .footer .nav-title {
      color: #919496;
      font-size: 12px;
      letter-spacing: .08em;
      margin: 20px 0;
      text-transform: uppercase;
    }

    .footer .nav li a {
      padding: 3px 0;
      margin: 0 0 12px;
    }

    .col-social {
      margin-top: 20px;
    }

    .footer .col-social ul {
      float: right;
    }

    .footer .col-social li {
      display: inline-block;
    }

    .footer .col-social li a {
      padding: 15px;
      margin-bottom: 12px;
      background-color: #222326;
      border-radius: 30px;
    }

    .footer .col-social a:hover {
      background-color: #222326;
    }

    .col-social a img {
      width: 24px;
      height: 24px;
    }

    .footer .nav-small a {
      color: #919496;
    }

    .footer .nav-small li a {
      float: left;
      font-size: 12px;
      font-weight: 400;
      padding: 12px;
      margin: 0;
    }

    .row-small {
      margin-top: 100px;
    }

    .footer .nav-small li:first-child a {
      padding-left: 0;
    }

    .flag-icon-us {
        background-image: url('https://sp-bootstrap.global.ssl.fastly.net/8.0.0/images/flags/us.svg');
    }

    .flag-icon {
      background-position: 50%;
      background-repeat: no-repeat;
      background-size: contain;
      display: inline-block;
      font-size: 18px;
      height: 1em;
      width: 1.33333333em;
    }

    .market, .copyright {
      color: #919496;
      font-size: 12px;
    }

    a.market {
      color: #919496;
      text-decoration: none;
    }

That's it folks!