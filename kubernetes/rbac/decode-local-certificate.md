# Decode Local certificate

```
cd
cd .kube
cat config
# copy client-certificate-data
```

```
echo LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURLVENDQWhHZ0F3SUJBZ0lJVGpPWWowbXpWMFl3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TkRFd01UQXdPVEV3TlRWYUZ3MHlOVEV3TVRBd09URTFOVFZhTUR3eApIekFkQmdOVkJBb1RGbXQxWW1WaFpHMDZZMngxYzNSbGNpMWhaRzFwYm5NeEdUQVhCZ05WQkFNVEVHdDFZbVZ5CmJtVjBaWE10WVdSdGFXNHdnZ0VpTUEwR0NTcUdTSWIzRFFFQkFRVUFBNElCRHdBd2dnRUtBb0lCQVFEUm1mZkkKVTdxNkN3bzFvRExoS2xzSXpWNU1LeHluV2lMV3NXeWk0dVluUGhqRXJ5MlZrOTFiN0trdGtNYm1Xc1RtMXNsTAphVzVGUENQRFlMRFNSWkJHd0NsQ0svV1FGNXJhbUxieG5icnJ6VUtuUWFaMnhpWmdNU2ppNGNZby9lQnJOdEFTCnhISnEyUVNpeU93QnhJOGhGdlQwTDhJa3FHZ3F6T2VXakZFcnY0MU8weXU2TzNYR0dyakR3Y2lIbXpRK3ZTVmYKZzhaNzV4UFRNcFZmUTU3QzM3Y2xRdHVMaVJ1WXNNSnFudUtYNjVtalF1TDNCVTJnai8vNTIwYVdsWXZHSDNTUwp4MkRadEhodFBSaFh5T2hJSlZyVzE0RXpqQ2UyblNJMjFDdEdZNndaT1pCU0w0ZFpWMDNseEFQUks0QTdDUlYwCkY5bFVLUFpkSDdrbGxDOW5BZ01CQUFHalZqQlVNQTRHQTFVZER3RUIvd1FFQXdJRm9EQVRCZ05WSFNVRUREQUsKQmdnckJnRUZCUWNEQWpBTUJnTlZIUk1CQWY4RUFqQUFNQjhHQTFVZEl3UVlNQmFBRkVobjFLQnpyeTc4TW5ZYwo4Z0VwcVYrSStsbWtNQTBHQ1NxR1NJYjNEUUVCQ3dVQUE0SUJBUUFOVmxreE04Wk5Eb2JqTzllUkNVYWU1dDFGClpURURDQTMxdEhQTWdYS3VQUlpyalhVUlFPTlcrc2VkK1dYU0pGVk1XYkdTMnlhWk5GblpnT1FtckVxQXltZU0KN3JSdnJaN3RmM1F3MTBXQWlUS1lpSnpwVjNwVGVvaFR0eDc2Z2VQejMwcGkxZ2pQNmRaajRiL3kwSmFZU0FXRQpSM3UyaGxSZGFKcklDK3Y1b1ZnRU1Kd0FaMnJCbnkvOExXNFJpcGxmUFo4MW5pRkJ6R010VmxWZW8wZ3V4cEI3CmhVQVdzS1lSZjZFdHZ4czNDaUQ3SVkzRGZWeWs2dXhZQXFKMjZpM3pQVDlNVG5ZWHpTTWJOT25kL0UzOFZ5RjcKeDVTRktmbnQ1dEFqNk9FVGJ0Y3RDb1dLejZWNHhmQ2JuM0FrcURweTN5bjhlMzA0Zyt4M2FiUXpMTFBkCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K base64 -d > out.crt
openssl x509 -in out.crt -text -noout
```
