# NAME 

Apache::Clean - mod\_perl interface into HTML::Clean

# SYNOPSIS

httpd.conf:

    PerlModule Apache::Clean

    <Location /clean>
       SetHandler perl-script
       PerlHandler Apache::Clean

       PerlSetVar  CleanLevel 3

       PerlSetVar  CleanOption shortertags
       PerlAddVar  CleanOption whitespace

       PerlSetVar  CleanCache On
    </Location>  

Apache::Clean is Filter aware, meaning that it can be used within
Apache::Filter framework without modification.  Just include the
directives

    PerlModule Apache::Filter
    PerlSetVar Filter On

and modify the PerlHandler directive accordingly...

# DESCRIPTION

Apache::Clean uses HTML::Clean to tidy up large, messy HTML, saving
bandwidth.  It is particularly useful with Apache::Compress for 
ultimate savings.

Only documents with a content type of "text/html" are affected - all
others are passed through unaltered.

# OPTIONS

Apache::Clean supports few options, most of which are based on
options from HTML::Clean.  Apache::Clean will only tidy up whitespace 
(via $h->strip) and will not perform other options of HTML::Clean
(such as browser compatibility).  See the HTML::Clean manpage for 
details.

- CleanLevel

    sets the clean level, which is passed to the level() method
    in HTML::Clean.

        PerlSetVar CleanLevel 9

    CleanLevel defaults to 3.

- CleanOption

    specifies the set of options which are passed to the options()
    method in HTML::Clean.

        PerlAddVar CleanOption shortertags
        PerlSetVar CleanOption whitespace

    CleanOption has do default.

- CleanCache

    sets the behavior of Apache::Clean in regards to proper
    cache header behavior.  this option is only meaningful
    when Apache::Clean is \_not\_ part of an Apache::Filter
    chain.

    mainly, CleanCache On enables Apache::Clean to
    set the Last-Modified, Content-Length, and Etag headers,
    as well as allowing it do decide whether a 304 response
    is allowed.  See recipe 6.6 in the mod\_perl Developer's
    Cookbook for a more detailed discussion on handling
    conditional and cache-based headers - the code is
    practically identical to what you will find there.

    The basic idea here is that although Apache::Clean is
    dynamically manipulating the content of the requested
    resource, the meaning of the document has not changed
    just because &lt;strong> was changed to &lt;b>.  If you
    disagree with this assessment you can set CleanCache to
    Off.

    CleanCache defaults to On.

# NOTES

Verbose debugging is enabled by setting $Apache::Clean::DEBUG=1
or greater.  To turn off all debug information, set your apache
LogLevel directive above info level.

This is alpha software, and as such has not been tested on multiple
platforms or environments.  It requires PERL\_LOG\_API=1, 
PERL\_FILE\_API=1, and maybe other hooks to function properly.

# FEATURES/BUGS

No known bugs or features at this time...

# SEE ALSO

perl(1), mod\_perl(3), Apache(3), HTML::Clean(3), Apache::Compress(3),
Apache::Filter(3)

# AUTHORS

Geoffrey Young <geoff@modperlcookbook.org>
Paul Lindner <paul@modperlcookbook.org>
Randy Kobes <randy@modperlcookbook.org>

# COPYRIGHT

Copyright (c) 2002, Geoffrey Young, Paul Lindner, Randy Kobes.  
All rights reserved.

This module is free software.  It may be used, redistributed
and/or modified under the same terms as Perl itself.

# HISTORY

This code is derived from the Cookbook::Clean and
Cookbook::TestMe modules available as part of
"The mod\_perl Developer's Cookbook".

For more information, visit http://www.modperlcookbook.org/