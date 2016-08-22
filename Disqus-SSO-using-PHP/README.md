<a id="top"></a>

# Disqus SSO using PHP

Sometimes we don't need the user to sign in again to Disqus when the user has already signed in through our website. This can be achieved by using SSO(Single Sign On).

First we need to create Public Key and Secret Key on Disqus, you can do this as follows:

- Create an account on https://disqus.com
- Now, go to https://disqus.com/api/applications/
- Create an application by filling out the form there.

After doing this you can directly check it using this:

```php
<?php
define('DISQUS_SECRET_KEY', 'Your_Secret_Key');
define('DISQUS_PUBLIC_KEY', 'Your_Public_Key');

/* userdata */
$data = array(
  "id" => "Some Id", //-> ID which is used by you to recognize the user
  "username" => "Set username", //-> Username you are using on your own site
  "email" => "user email addredd" //-> email address of user
);
 
function dsq_hmacsha1($data, $key) {

  $blocksize=64;
  $hashfunc='sha1';
  
  if (strlen($key)>$blocksize)
    $key=pack('H*', $hashfunc($key));
  
  $key=str_pad($key,$blocksize,chr(0x00));
  $ipad=str_repeat(chr(0x36),$blocksize);
  $opad=str_repeat(chr(0x5c),$blocksize);
  $hmac = pack(
            'H*',$hashfunc(
              ($key^$opad).pack(
                'H*',$hashfunc(
                  ($key^$ipad).$data
                )
              )
            )
          );
   return bin2hex($hmac);

}
 
$message = base64_encode(json_encode($data));
$timestamp = time();
$hmac = dsq_hmacsha1($message . ' ' . $timestamp, DISQUS_SECRET_KEY);

?>
<html>
  <head>
    <title>Demo - Disqus SSO using PHP</title>
    <script type="text/javascript">
      var disqus_config = function() {
        this.page.remote_auth_s3 = "<?php echo "$message $hmac $timestamp"; ?>";
        this.page.api_key = "<?php echo DISQUS_PUBLIC_KEY; ?>";
      };
      
      /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
      var disqus_shortname = 'EXAMPLE'; // required: replace EXAMPLE with your forum shortname

      /* * * DON'T EDIT BELOW THIS LINE * * */
      (function() {
        var dsq = document.createElement('script'); dsq.type = 'text/javascript'; 
        dsq.async = true;
        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
      })();
    </script>
    <noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
  </head>
  <body>
    <h1>Demo - Disqus SSO using PHP</h1>
    <div id="disqus_thread"></div>
  </body>
</html>
```

#### One Last thing:  

This will only work when Disqus has Enable SSO for yor site. For this you can visit: https://disqus.com/support/

A form will appear, 

- Select the site for which you are applying.
- Select `Other` in the `Platform` dropdown which will appear after you done with above step.
- Select `Enable SSO` from `What can we help you with?` dropdown.
- Write the `Subject`
- As you write the subject a link will appear `Still having issues? Send us more details.`, click on that.
- Fill in the form which appear and press send.

After you send the mail, only thing is to wait for Disqus to reply back. Sit tight.

[Top](#top)

---

## The End
