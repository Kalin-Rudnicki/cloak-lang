
Ignoring "\n" at this point

```
File              : NamespaceFlat

NamespaceFlat     : "namespace" ScopeName NamespaceContents
NamespaceWrap     : "namespace" ScopeName "{" NamespaceContents "}"
Namespace         : NamespaceFlat
                  | NamespaceWrap

Class             : MaybeAccess "class" "(" ClassParams ")" ClassExts "{" ClassContents1 "}"
                  | MaybeAccess "class" ClassExts "{" ClassContents2 "}"

MaybeAccess       : "public"
                  | "private"
                  | "protected"
                  |


MaybeDocComment   : DocComment
                  |
DocComment        : "\**" docCommentStr "*\"

```
