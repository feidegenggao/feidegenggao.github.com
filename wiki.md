---
layout: page
title: Wiki
---
<div class="wiki">
    <h2>Javascript</h2>
    <ul class="hide">
       <li><a href="http://www.addyosmani.com/resources/essentialjsdesignpatterns/book/" title="Javscript设计模式">Javscript设计模式</a></li>
        <li>JSON工具：</li>
        <ul>
            <li><a href="http://www.jsonlint.com/">JSONLint</a> - The JSON Validator</li>
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
