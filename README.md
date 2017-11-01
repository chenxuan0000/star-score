## 纯css实现的star click 评分  基于jq做了向下兼容

```html

<link rel="stylesheet" type="text/css" href="css/starability.css" /> //css
<section>
        <div class="checkmark" id="checkmark">
            <input type="radio" title="Amazing" name="rating" value="5.0" class="radio5" />
            <label></label>
            <input type="radio" title="Very good" name="rating" value="4.0" class="radio4" />
            <label></label>
            <input type="radio" title="Average" name="rating" value="3.0" class="radio3" />
            <label></label>
            <input type="radio" title="Not good" name="rating" value="2.0" class="radio2" />
            <label></label>
            <input type="radio" title="Terrible" name="rating" value="1.0" class="radio1" />
            <label></label>
        </div>
</section>

```

```javascript
//向下兼容处理 ie8
<script type="text/javascript" src="jquery-1.11.0.min.js"></script> 
(function($) {
    // 加上评分数
    var $checkmark = $("#checkmark");
    $checkmark.on('click', 'input', function() {
        var $this = $(this),
            scoreStr = "<span class='goal'>" + this.value + "</span>";
        $checkmark.children("label").empty();
        $this.next().append(scoreStr);
    });
    // ie9下生效
    if (navigator.appName == "Microsoft Internet Explorer" && parseInt(navigator.appVersion.split(";")[1].replace(/[ ]/g, "").replace("MSIE", "")) < 9) {
        var $checkmark = $("#checkmark"),
            ClickStar = 1,
            $dom = '';

        var clearStar = function() {
            $dom.addClass('selected').nextAll('label').addClass('selected')
                .end().prevAll('label').removeClass('selected');
        };

        $checkmark.on('mousemove', 'input', function() {
            $(this).addClass('selected').nextAll('label').addClass('selected')
                .end().prevAll('label').removeClass('selected');
        });

        $checkmark.on('click', 'input', function() {
            var $this = $(this);
            $dom = $this;
            $checkmark.on('mouseleave', clearStar);
        });

    }

})(jQuery);

```