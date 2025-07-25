SELECT
    s.sid,
    s.serial#,
    s.username,
    s.machine,
    o.object_name,
    l.type,
    l.lmode,
    l.request
FROM
    v$session s
JOIN v$lock l ON s.sid = l.sid
JOIN dba_objects o ON l.id1 = o.object_id
WHERE
    o.object_name = 'YOUR_TABLE_NAME'
    AND o.owner = 'TABLE_OWNER';