---
layout: page
title: Wiki
---
<div class="wiki">
<h2>效率工具</h2>
    <ul class="hide">
        <li><a href="http://markdown.tw/" title="Markdown语法">Markdown语法</a></li>
        <li>VIM</li>
        <ul>
            <li><a href="http://wiki.hotoo.me/Vim.html">Vim - 闲耘</a>Vim - 闲耘</li>
        </ul>

        <li>Git</li>
        <ul>
        <li><a href="http://gitref.cyj.me/zh/">Git参考手册</a>Git参考手册</li>
        </ul>
     </ul>
</div>
<script type="text/javascript">
$(document).ready(function(){
        $('#content a').each(function(index,element){
            var href = $(this).attr('href');
            if(href.indexOf('#') == 0){
            }else if ( href.indexOf('/') == 0 || href.toLowerCase().indexOf('beiyuu.com')>-1 ){
            $(this).attr('target','_blank');
            }else{
            $(this).attr('target','_blank');
            $(this).addClass('external');
            }
            });
        $('body').delegate('h2','click',function(e){
            e.preventDefault();
            $(this).next('ul').toggle();
            });
        });
</script>
