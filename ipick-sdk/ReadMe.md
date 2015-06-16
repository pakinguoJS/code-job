# Documentation for ipick-sdk #

This document is just for ipick-sdk.js(v1.3.0). Please contact [me](mailto:pakinguo@tencent.com) to get the resource code file.

----------

<br>
# How to use ipick-sdk? #

Method 1(Traditional):

    <script type="text/javascript" src="ipick-sdk.js"></script>
	document.getElementById('click').onclick = function(){
		ipick.callShare();
	}

Method 2(Use cmd or amd):

    var ipick = require('ipick-sdk.js');
	document.getElementById('click').onclick = function(){
		ipick.callShare();
	}


----------

<br>
# API LIST: #

1. [error](#ipickerror): This function provide a callback parameter for dispose technology limited in chrome browser.
2. [config](#ipickconfig): Setting which type to call iPick(either 'iframe' of 'a' element).
3. [setShareConfig](#ipicksetshareconfig): Set shared config for top right corner share button of in-app webview.
4. [callShare](#ipickcallshare): Trigger share function directly.
5. [callRestaurantDetail](#ipickcallrestaurantdetail): Call restaurant detail by restaurant's id.
6. [callSearchList](#ipickcallsearchlist): Call search result of restaurant list by condition parameters.
7. [callInappWebview](#ipickcallinappwebview): Call in-app webview.
8. [callArticleDetail](#ipickcallarticledetail): Call article(critics) detail by article's id.
9. [callArticleList](#ipickcallarticlelist): Call article list by list's id.
10. [callBloggerDetail](#ipickcallbloggerdetail): Call blogger detail by blogger's id.
11. [callRecommendList](#ipickcallrecommendlist): Call recommend list on home page by recomment list's id.
12. [callBindAccount](#ipickcallbindaccount): Call up the accound binding page of iPick.
13. [callHomepage](#ipickcallhomepage): Call up the home page of iPick.
14. [callMyFeeds](#ipickcallmyfeeds): Call Food Moments on home page.
15. [callUserFeeds](#ipickcalluserfeeds): Call user's feeds by user's id.
16. [callRestaurantFeeds](#ipickcallrestaurantfeeds): Call restaurant's feeds by restaurant's id.
17. [callFeedsDetail](#ipickcallfeedsdetail): Call a feed detail by feed's id.
18. [callSystemMessage](#ipickcallsystemmessage): Call system message page.
19. [callUserMessage](#ipickcallusermessage): Call user message page.
20. [callCommentDetail](#ipickcallcommentdetail): Call single comment detail by comment's id.


----------
<br>

<br>
## ipick.error ##
	/**
 	 * Since iframe call up the nation app is not supported, while using it in chrome, this api provides a hack way.
 	 * @param {function} callback
 	 */
    ipick.error(callback);

	e.g.
	ipick.error(function(){ alert("Your borwser isn't supported our function!"); });
	ipick.error(function(){ ipick.config({method: true}) });

<br>
## ipick.config ##
	/**
	 * Because of production requirements that is required to 
	 * call up iPick while user has been installed it, 
	 * or redirect to download page while user doesn't install it,
	 * the sdk is default to follow the requirements in almost all browsers except 'Chrome'.
	 * It's default to set 'method' false.
 	 * @param {object} obj just support 'method' property so far. 'true' for use 'a' element, 'false' to use 'iframe'
 	 */
	ipick.config(obj); 

	e.g.
	// When in Chrome, change to use 'a' element way to call iPick, even against the requirements.
	ipick.error(function(){ ipick.config({method: true}) }); 

<br>
## ipick.setShareConfig ##
    /**
     * Set shared config for top right corner share button of in-app webview.
     * After setting, it will be used when user click the top right corner share button of in-app webview.
     * It's different from ipick.callShare.
     * @param {object} config
     */
    ipick.setShareConfig(config);
	config's data structure as follow:
	{
		title: '',	// share title
		icon: '',	// share icon url
		desc: '',	// share description
		link: ''	// share url
	}

	e.g.
	ipick.setShareConfig({
		title: 'test',
		icon: 'http://htpic.tc.qq.com/IBG_41021777a2b3298e5fde0e3f1e52103c',
		desc: 'share setting',
		link: location.href
	});

<br>
## ipick.callShare ##
	/**
	 * Direct way to call share function.
	 * @param {object} config same as ipick.setShareConfig
	 */
	ipick.callShare(config);
	
	e.g.
	document.getElementById('share').onclick = function(){
		ipick.callShare({
			title: 'test',
			icon: 'http://htpic.tc.qq.com/IBG_41021777a2b3298e5fde0e3f1e52103c',
			desc: 'share setting',
			link: location.href
		})
	}

<br>
## ipick.callRestaurantDetail ##
    /**
     * @param {number} rid restaurant's id
     * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
     * @param {number} login when it sets to 1, the iPick will call up the login page while user doesn't login, default 0
     */
    ipick.callRestaurantDetail(rid[, downloadUrl, login]);

	e.g.
	ipick.callRestaurantDetail(100016, 'https://itunes.apple.com/app/ipick/id912765938?l=zh&ls=1&mt=8', 1);

<br>
## ipick.callSearchList ##
    /**
     * @param {object} condition search condition
     * @param {string} title result title
     * @param {boolean} hidefilter whether to hide the top right corner filter button, default false
     * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
     * @param {number} login when it sets to 1, the iPick will call up the login page while user doesn't login, default 0
     */
    ipick.callSearchList(condition, title, hidefilter[, downloadUrl, login]);

	e.g.
	ipick.callSearchList({
        "keyword":"@secret@(f_rid:(303480^35 303521^34 303366^33))",
        "channelid": 10000
    }, 'test', true, null, 1);

<br>
## ipick.callInappWebview ##
	/**
	 * @param {string} url the web url to show
	 * @param {number} showbtn whether to hide the top right corner button, 1 is to show, 0 is to hide, default 1
	 * @param {number} buttontype type of top right corner button, 1 is to refresh, 2 is to share, default 1
	 * @param {number} browser whether to open in out-side browser, 1 is yes, 0 is no, default 0
	 * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
	 * @param {number} login when it sets to 1, the iPick will call up the login page while user doesn't login, default 0
	 */
	ipick.callInappWebview(url, showbtn, buttontype, browser[, downloadUrl, login]);

	e.g.
	ipick.callInappWebview('https://github.com/pakinguoJS/code-job/tree/master/ipick-sdk', 1, 2, 0, null, 1);

<br>
## ipick.callArticleDetail ##
    /**
     * @param {string} url url of article detail
     * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
     * @param {number} login when it sets to 1, the iPick will call up the login page while user doesn't login, default 0
     */
    ipick.callArticleDetail(url[, downloadUrl, login]);

	e.g.
	ipick.callArticleDetail('http://ipick1.wechat.com/web23/index.php/article/detail/348?channel=1&lang=en');

<br>
## ipick.callArticleList ##
    /**
     * @param {string} listid list's id
     * @param {string} name list's title
     * @param {number} canChangeCategory whether to show the top right corner classify button, 1 is to show, 0 is to hide, default 0
     * @param {number} sortindex sort index, optional
     * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
     * @param {number} login when it sets to 1, the iPick will call up the login page while user doesn't login, default 0
     */
    ipick.callArticleList(listid, [name, canChangeCategory, sortindex, downloadUrl, login]);

<br>
## ipick.callBloggerDetail ##
    /**
     * @param {string} id blogger's id
     * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
     * @param {number} login when it sets to 1, the iPick will call up the login page while user doesn't login, default 0
     */
    ipick.callBloggerDetail(id[, downloadUrl, login]);


<br>
## ipick.callRecommendList ##
    /**
     * @param {string} listid list's id
     * @param {string} title list's title
     * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
     * @param {number} login when it sets to 1, the iPick will call up the login page while user doesn't login, default 0
     */
    ipick.callRecommendList(listid, title[, downloadUrl, login]);


<br>
## ipick.callBindAccount ##
    /**
     * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
     */
    ipick.callBindAccount([downloadUrl]);


<br>
## ipick.callHomepage ##
	/**
	 * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
	 * @param {number} login when it sets to 1, the iPick will call up the login page while user doesn't login, default 0
	 */
	ipick.callHomepage([downloadUrl, login]);


<br>
## ipick.callMyFeeds ##
	/**
	 * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
	 */
	ipick.callMyFeeds([downloadUrl]);


<br>
## ipick.callUserFeeds ##
    /**
     * @param {string} uid user's id
     * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
     */
    ipick.callUserFeeds(id[, downloadUrl]);


<br>
## ipick.callRestaurantFeeds ##
    /**
     * @param {string} rid restaurant's id
     * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
     */
    ipick.callRestaurantFeeds(rid[, downloadUrl]);


<br>
## ipick.callFeedsDetail ##
    /**
     * @param {string} id feed's id
     * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
     */
    ipick.callFeedsDetail(id[, downloadUrl]);


<br>
## ipick.callSystemMessage ##
    /**
     * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
     * @param {number} login when it sets to 1, the iPick will call up the login page while user doesn't login, default 0
     */
    ipick.callSystemMessage([downloadUrl, login])


<br>
## ipick.callUserMessage ##
    /**
     * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
     */
    ipick.callUserMessage([downloadUrl]);


<br>
## ipick.callCommentDetail ##
    /**
     * @param {number} id comment's id
     * @param {string} downloadUrl when user trigger this api without installed iPick, the web page will redirect to this url. Default NULL
     */
    ipick.callCommentDetail(id[, downloadUrl]);


