# todolist is based on http://www.mytinytodo.net/
todolist  support php7+

How to install:

## 1. create 4 tables in your database:
```sql
CREATE TABLE `mtt_lists` (
  `id` int(10) UNSIGNED NOT NULL,
  `uuid` char(36) NOT NULL DEFAULT '',
  `ow` int(11) NOT NULL DEFAULT '0',
  `name` varchar(50) NOT NULL DEFAULT '',
  `d_created` int(10) UNSIGNED NOT NULL DEFAULT '0',
  `d_edited` int(10) UNSIGNED NOT NULL DEFAULT '0',
  `sorting` tinyint(3) UNSIGNED NOT NULL DEFAULT '0',
  `published` tinyint(3) UNSIGNED NOT NULL DEFAULT '0',
  `taskview` int(10) UNSIGNED NOT NULL DEFAULT '0'
) ENGINE=MyISAM DEFAULT CHARSET=utf8;


ALTER TABLE `mtt_lists`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `uuid` (`uuid`);


ALTER TABLE `mtt_lists`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT;
COMMIT;

CREATE TABLE `mtt_todolist` (
  `id` int(10) UNSIGNED NOT NULL,
  `uuid` char(36) NOT NULL DEFAULT '',
  `list_id` int(10) UNSIGNED NOT NULL DEFAULT '0',
  `d_created` int(10) UNSIGNED NOT NULL DEFAULT '0',
  `d_completed` int(10) UNSIGNED NOT NULL DEFAULT '0',
  `d_edited` int(10) UNSIGNED NOT NULL DEFAULT '0',
  `compl` tinyint(3) UNSIGNED NOT NULL DEFAULT '0',
  `title` varchar(250) NOT NULL,
  `note` text,
  `prio` tinyint(4) NOT NULL DEFAULT '0',
  `ow` int(11) NOT NULL DEFAULT '0',
  `tags` varchar(600) NOT NULL DEFAULT '',
  `tags_ids` varchar(250) NOT NULL DEFAULT '',
  `duedate` date DEFAULT NULL
) ENGINE=MyISAM DEFAULT CHARSET=utf8;

ALTER TABLE `mtt_todolist`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `uuid` (`uuid`),
  ADD KEY `list_id` (`list_id`);

ALTER TABLE `mtt_todolist`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT;
COMMIT;

CREATE TABLE `mtt_tags` (
  `id` int(10) UNSIGNED NOT NULL,
  `name` varchar(50) NOT NULL
) ENGINE=MyISAM DEFAULT CHARSET=utf8;

ALTER TABLE `mtt_tags`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `name` (`name`);

ALTER TABLE `mtt_tags`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=2;
COMMIT;

CREATE TABLE `mtt_tag2task` (
  `tag_id` int(10) UNSIGNED NOT NULL,
  `task_id` int(10) UNSIGNED NOT NULL,
  `list_id` int(10) UNSIGNED NOT NULL
) ENGINE=MyISAM DEFAULT CHARSET=utf8;

ALTER TABLE `mtt_tag2task`
  ADD KEY `tag_id` (`tag_id`),
  ADD KEY `task_id` (`task_id`),
  ADD KEY `list_id` (`list_id`);
COMMIT;
```

## 2. visit your host/index.php

ps:makesure tmp could be written
chmod 777 tmp