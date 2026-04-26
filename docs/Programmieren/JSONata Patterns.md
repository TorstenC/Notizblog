# JSONata Patterns
<!-- markdownlint-disable MD033 -->
<table>
  <tr role='columnheader'>
    <td>Input</td>
    <td>JSONata</td>
    <td>Out</td>
  </tr>
  <tr>
    <td colspan='3'>
      Einfaches Hello World Beispiel
    </td>
  </tr>
  <tr>
    <td>
      <pre>{
  'a': {
    'b': 1,
    'c': 2
  }
}</pre>
    </td>
    <td>
      <pre>
{
  'x': a.b,
  'y': a.c
}</pre>
    </td>
    <td>
      <pre>{
  'x': 1,
  'y': 2
}</pre>
    </td>
  </tr>
  <tr>
    <td colspan='3'>
      <b>LeanIX Subscription Matrix</b><br/>
      Extrahiert Verantwortliche und flacht Rollen-Arrays zu einer Matrix (Liste) ab.
    </td>
  </tr>
  <tr>
    <td>
      <pre>
{
  'node': {
    'subscriptions': {
      'edges': [
        {
          'node': {
            'type': 'RESPONSIBLE',
            'user': {
              'firstName': 'Jane',
              'lastName': 'Doe',
              'email': 'jane@doe.com'
            },
            'roles': [
              { 'name': 'Owner', 'comment': 'Top' },
              { 'name': 'Editor', 'comment': null }
            ]
          }
        },
        {
          'node': {
            'type': 'RESPONSIBLE',
            'user': {
              'firstName': 'Max',
              'lastName': 'Mustermann',
              'email': 'max@test.de'
            },
            'roles': []
          }
        }
      ]
    }
  }
}</pre>
    </td>
    <td>
      <pre>
node.subscriptions.edges.node[type='RESPONSIBLE'].(
  $u := user.{ 
    'firstName': firstName, 
    'lastName': lastName, 
    'email': email 
  };
  'roles':
    ( roles ) 
    ? roles.($merge([$u, {
        'role': name,
        'comment': comment
      }])) 
    : $u
)</pre>
    </td>
    <td>
      <pre>
[
  {
    'firstName': 'Jane',
    'lastName': 'Doe',
    'email': 'jane@doe.com',
    'role': 'Owner',
    'comment': 'Top'
  },
  {
    'firstName': 'Jane',
    'lastName': 'Doe',
    'email': 'jane@doe.com',
    'role': 'Editor',
    'comment': null
  },
  {
    'firstName': 'Max',
    'lastName': 'Mustermann',
    'email': 'max@test.de'
  }
]</pre>
    </td>
  </tr>
</table>
<!-- <file:///home/eb0crul/Dokumente/source-gluc/temp/table-JSONata-patterns.html> -->
