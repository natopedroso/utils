# Remove permissões amplas
icacls ".keys\sos01" /inheritance:r
# Dá permissão total apenas para você
icacls ".keys\sos01" /grant:r "$($env:USERNAME):R"
