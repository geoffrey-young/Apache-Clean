# NAME 

Apache::Clean - interface into HTML::Clean for mod\_perl 2.0

# SYNOPSIS

httpd.conf:

    PerlModule Apache::Clean

    Alias /clean /usr/local/apache2/htdocs
    <Location /clean>
      PerlOutputFilterHandler Apache::Clean

      PerlSetVar CleanOption shortertags
      PerlAddVar CleanOption whitespace
    </Location>

# DESCRIPTION

Apache::Clean uses HTML::Clean to tidy up large, messy HTML, saving
bandwidth. 

Only documents with a content type of "text/html" are affected - all
others are passed through unaltered.

For more information, see

    http://www.perl.com/pub/a/2003/04/17/filters.html

# OPTIONS

Apache::Clean supports few options - all of which are based on
options from HTML::Clean.  Apache::Clean will only tidy up whitespace 
(via $h->strip) and will not perform other options of HTML::Clean
(such as browser compatibility).  See the HTML::Clean manpage for 
details.

- CleanLevel

    sets the clean level, which is passed to the level() method
    in HTML::Clean.

        PerlSetVar CleanLevel 9

    CleanLevel defaults to 1.

- CleanOption

    specifies the set of options which are passed to the options()
    method in HTML::Clean - see the HTML::Clean manpage for a complete
    list of options.

        PerlSetVar CleanOption shortertags
        PerlAddVar CleanOption whitespace

    CleanOption has no default.

# NOTES

This is alpha software, and as such has not been tested on multiple
platforms or environments.

# FEATURES/BUGS

probably lots - this is the preliminary port to mod\_perl 2.0

# SEE ALSO

perl(1), mod\_perl(3), Apache(3), HTML::Clean(3)

# AUTHOR

Geoffrey Young <geoff@modperlcookbook.org>

# COPYRIGHT

Copyright (c) 2005, Geoffrey Young
All rights reserved.

This module is free software.  It may be used, redistributed
and/or modified under the same terms as Perl itself.

# HISTORY

This code is derived from the Cookbook::Clean and
Cookbook::TestMe modules available as part of
"The mod\_perl Developer's Cookbook".

For more information, visit http://www.modperlcookbook.org/
