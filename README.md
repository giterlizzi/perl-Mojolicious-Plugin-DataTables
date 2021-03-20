[![Release](https://img.shields.io/github/release/giterlizzi/perl-Mojolicious-Plugin-DataTables.svg)](https://github.com/giterlizzi/perl-Mojolicious-Plugin-DataTables/releases) [![Actions Status](https://github.com/giterlizzi/perl-Mojolicious-Plugin-DataTables/workflows/linux/badge.svg)](https://github.com/giterlizzi/perl-Mojolicious-Plugin-DataTables/actions) [![Actions Status](https://github.com/giterlizzi/perl-Mojolicious-Plugin-DataTables/workflows/macos/badge.svg)](https://github.com/giterlizzi/perl-Mojolicious-Plugin-DataTables/actions) [![License](https://img.shields.io/github/license/giterlizzi/perl-Mojolicious-Plugin-DataTables.svg)](https://github.com/giterlizzi/perl-Mojolicious-Plugin-DataTables) [![Starts](https://img.shields.io/github/stars/giterlizzi/perl-Mojolicious-Plugin-DataTables.svg)](https://github.com/giterlizzi/perl-Mojolicious-Plugin-DataTables) [![Forks](https://img.shields.io/github/forks/giterlizzi/perl-Mojolicious-Plugin-DataTables.svg)](https://github.com/giterlizzi/perl-Mojolicious-Plugin-DataTables) [![Issues](https://img.shields.io/github/issues/giterlizzi/perl-Mojolicious-Plugin-DataTables.svg)](https://github.com/giterlizzi/perl-Mojolicious-Plugin-DataTables/issues) [![Coverage Status](https://coveralls.io/repos/github/giterlizzi/perl-Mojolicious-Plugin-DataTables/badge.svg)](https://coveralls.io/github/giterlizzi/perl-Mojolicious-Plugin-DataTables)

# Mojolicious::Plugin::DataTables

## Usage

```.pl
# Mojolicious
$self->plugin('DataTables');

# Mojolicious::Lite
plugin 'DataTables';

helper sql => sub { state $pg = Mojo::Pg->new('postgresql://postgres@/test') };

get '/users_table' => sub {

    my $c = shift;
    my $sql = $c->sql;

    my $dt_ssp = $c->datatable->ssp(
        table   => 'users',
        sql     => $sql,
        options => [
            {
                label => 'UID',
                db    => 'uid',
                dt    => 0,
            },
            {
                label => 'e-Mail',
                db    => 'mail',
                dt    => 1,
            },
            {
                label => 'Status',
                db    => 'status',
                dt    => 2,
            },
        ]
    ));

    $c->render(json => $dt_ssp);
};

```

```.html
@@ template.html.ep

<html>
<head>
    <%= datatables_js %>
    <%= datatables_css %>
</head>
<body>
    <table id="users_table" class="display" style="width:100%">
        <thead>
            <th>UID</th>
            <th>e-Mail</th>
            <th>Status</th>
        </thead>
    </table>

    <script>
        jQuery('#users_table').DataTable({
            serverSide : true,
            ajax       : '/users_table',
        });
    </script>
</body>
</html>
```

## Installation

To install this module type the following:

    perl Makefile.PL
    make
    make test
    make install

## Copyright

Copyright (C) 2020-2021 by Giuseppe Di Terlizzi
