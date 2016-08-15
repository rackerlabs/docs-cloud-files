.. _absolute-limits:

===============
Absolute limits
===============

Absolute limits control the total number of specific objects that a user can
have or process in Cloud Files. Absolute limits are fixed.

The following table lists the absolute limits in Cloud Files.

+-----------------------+----------------------------------+------------------+
| Name                  | Description                      | Limit            |
+=======================+==================================+==================+
| Containers per        | Maximum number of containers     | 500,000          |
| account               | per account                      | containers       |
+-----------------------+----------------------------------+------------------+
| Container listing     | Maximum number of containers     | 10,000 containers|
|                       | that can be listed at one time   |                  |
+-----------------------+----------------------------------+------------------+
| Pseudo hierarchical   | Simulated hierarchical structure | No limit         |
| folders and           | within a single container,       |                  |
| directories           | created by adding a forward      |                  |
|                       | slash (``/``) in the object name |                  |
+-----------------------+----------------------------------+------------------+
| Account, container,   | Maximum metadata limits          | 90 distinct      |
| and object metadata   |                                  | metadata items at|
| limits                |                                  | the most. Each   |
|                       |                                  | piece of metadata|
|                       |                                  | can have a       |
|                       |                                  | 128-character    |
|                       |                                  | name             |
|                       |                                  | length with a 256|
|                       |                                  | maximum value    |
|                       |                                  | length. The total|
|                       |                                  | length of all    |
|                       |                                  | names and values |
|                       |                                  | cannot exceed    |
|                       |                                  | 4096 bytes.      |
+-----------------------+----------------------------------+------------------+
| Number of object      | Maximum number of object         | 1,000 object     |
| segments per static   | segments per SLO                 | segments         |
| large object (SLO)    |                                  |                  |
+-----------------------+----------------------------------+------------------+
| TTL for a CDN-enabled | Maximum TTL for a CDN-enabled    | 1 year           |
| container             | container                        | (31,536,000      |
|                       |                                  | seconds)         |
+-----------------------+----------------------------------+------------------+
| Container name length | Maximum length of container name | 256 bytes        |
+-----------------------+----------------------------------+------------------+
| Object name length    | Maximum length of object name    | 1024 bytes       |
+-----------------------+----------------------------------+------------------+
| Upload limit for a    | Maximum object size for an       | 5 GB (For larger |
| request               | upload in a single request       | files, create a  |
|                       |                                  | manifest file.)  |
+-----------------------+----------------------------------+------------------+
| CDN file size limit   | Maximum size of file that can be | 10 GB            |
|                       | served from CDN                  |                  |
+-----------------------+----------------------------------+------------------+
| Rate limit for write  | Maximum number of write          | 100 write        |
| operations            | operations per second per        | operations per   |
|                       | container, where a write         | second per       |
|                       | operation is a **COPY**,         | container        |
|                       | **DELETE**, **POST**, or         |                  |
|                       | **PUT**. If you reach this rate  |                  |
|                       | limit, Cloud Files slows the     |                  |
|                       | processing of write requests for |                  |
|                       | the container to 100 write       |                  |
|                       | operations per second per        |                  |
|                       | container.                       |                  |
+-----------------------+----------------------------------+------------------+
