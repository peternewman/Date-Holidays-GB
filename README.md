# NAME

Date::Holidays::GB - Determine British holidays - Current UK public and bank holiday dates up to 2016

# SYNOPSIS

    use Date::Holidays::GB qw/ holidays is_holiday /;

    # All UK holidays
    my $holidays = holidays( year => 2013 );

    # Holidays in England & Wales and Scotland
    my $holidays = holidays( year => 2013, regions => [ 'EAW', 'SCT' ] );

    if (is_holiday(
            year => 2013, month => 12, day => 25,
            regions => [ 'EAW', 'SCT' ] )
    ) {
        print "No work today!";
    }

# DESCRIPTION

A [Date::Holidays](https://metacpan.org/pod/Date::Holidays) style package updated with the British bank holiday dates now
published at [https://www.gov.uk/bank-holidays](https://www.gov.uk/bank-holidays). Holidays may apply to all
regions, or some combination - see the `regions` parameter for more details.

Module is named with correct ISO-3166-1 code for the United Kingdom: "GB"
(Great Britain)

To just work with holiday days for a single region, use one of the subclasses:
[Date::Holidays::GB::EAW](https://metacpan.org/pod/Date::Holidays::GB::EAW), [Date::Holidays::GB::NIR](https://metacpan.org/pod/Date::Holidays::GB::NIR), or
[Date::Holidays::GB::SCT](https://metacpan.org/pod/Date::Holidays::GB::SCT).

# EXPORTS

Exports `holidays` and `is_holiday` on demand. Also can export the aliases
`gb_holidays` and `is_gb_holiday`.

# METHODS

Both `is_holiday` and `holidays` take either an argument list or hash of
named arguments.

The named arguments are `year`, `month`, `day`, and `region`. `region`
should be either omitted (to search all regions) or an arrayref of the UK
regions that you are interested in, as ISO-3166-2 codes.

The argument list should be in the following order: year, month, day, and
(optionally) regions.

Note that you will need to specify region(s) to make correct use of this
module!

## holidays

    # year, month, day, [regions]
    my $holidays = Date::Holidays::GB->holidays( @args );

or

    # ( year => ..., month => ..., day => ..., [ regions => \@. .. ] )
    my $holidays = Date::Holidays::GB->holidays( %args );

Returns hashref of holiday dates, values are a string listing the holiday(s)
taking place on that date, with the region name(s) in parenthesis.

Holidays that occur in all regions are returned with a single canonical name,
taken from the name in England & Wales.

Date keys are in the format MMDD, as per the behaviour of [Date::Holidays](https://metacpan.org/pod/Date::Holidays).

## is\_holiday

    # year, month, day, [regions]
    my $holiday = Date::Holidays::GB->is_holiday( @args );

or

    # ( year => ..., month => ..., day => ..., [ regions => \@. .. ] )
    my $holiday = Date::Holidays::GB->is_holiday( %args );

Returns the holiday details (as per `holidays`) but for a single date.
Returns false if the specified date is not a holiday in the appropriate
region(s).

## date\_generated

    print Date::Holidays::GB->date_generated;

Prints the date that the data was downloaded, in YYYY-MM-DD format.

# ISO-3166-2 REGION CODES

Valid codes for the regions that make up ISO-3166-1 "GB" are:

- EAW - England & Wales
- SCT - Scotland
- NIR - Northern Ireland

# GENERATING THE DATA

The source for this package is generated via a script, included with the
distribution (["generate\_date\_holidays\_gb.pl" in share](https://metacpan.org/pod/share#generate_date_holidays_gb.pl)). This downloads the
latest iCal files from [http://www.gov.uk/](http://www.gov.uk/), and could be used to
update/alter the package if necessary.

# SEE ALSO

- [Date::Holidays](https://metacpan.org/pod/Date::Holidays)
- [Date::Holidays::UK](https://metacpan.org/pod/Date::Holidays::UK) - not currently updated
- [Date::Holidays::UK::EnglandAndWales](https://metacpan.org/pod/Date::Holidays::UK::EnglandAndWales) - not currently updated
- [Date::Holidays::EnglandWales](https://metacpan.org/pod/Date::Holidays::EnglandWales) - not currently updated

# SUPPORT

## Bugs / Feature Requests

Please report any bugs or feature requests through the issue tracker
at [https://github.com/mjemmeson/Date-Holidays-GB/issues](https://github.com/mjemmeson/Date-Holidays-GB/issues).
You will be notified automatically of any progress on your issue.

## Source Code

This is open source software.  The code repository is available for
public review and contribution under the terms of the license.

[https://github.com/mjemmeson/Date-Holidays-GB](https://github.com/mjemmeson/Date-Holidays-GB)

    git clone https://github.com/mjemmeson/Date-Holidays-GB.git

# AUTHOR

Michael Jemmeson <mjemmeson@cpan.org>

# COPYRIGHT

This software is copyright (c) 2013-2015 by Michael Jemmeson.

# LICENSE

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
