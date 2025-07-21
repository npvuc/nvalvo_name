

---

# Character_Example

Arbortext Editor writes out the copyright character entity as a character ( © ) if the commands are set as follows:

```
set entityinputconvert=on
set writenonasciichar=char
```

or

```
set entityoutputconvert=on
set writenonasciichar=char
```



---

# Entity_Reference_Example

Arbortext Editor writes out the copyright character entity as an entity reference ( &copy; ) if the commands are set as follows:

```
set entityinputconvert=on
set writenonasciichar=entref
```

or

```
set entityoutputconvert=on
set writenonasciichar=entref
```

or

```
set entityinputconvert=off
set entityoutputconvert=off
```

If either entityinputconvert or entityouputconvert is set to on and writenonasciichar is set to entref , Arbortext Editor converts entity references to characters and then converts them back to entity references. As a result of this conversion, the name of the entity reference that Arbortext Editor writes out may be different than the name of the entity reference that was read in.

However, if set entityinputconvert and set entityoutputconvert are off , Arbortext Editor preserves character entities and writes them out as entity references (it doesn't matter what the value of set writenonasciichar is). In this situation, the name of the entity reference that Arbortext Editor writes out is the same as the one that was read in since no conversion occurred.

## Related Topics

- • set entityinputconvert command

- • set entityoutputconvert command

- • write command

- • Storing non-ASCII characters



---

# Numeric_Reference_Example

Arbortext Editor writes out the copyright character entity as a numeric reference ( &#xa9 ) if the commands are set as follows:

```
set entityinputconvert=on
set writenonasciichar=numref
```

or

```
set entityoutputconvert=on
set writenonasciichar=numref
```