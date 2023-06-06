# System-admin-note
C#

using Microsoft.Win32;

// Pridedame Network Service prie S-1-5-20 registro rakto permisijų
RegistryKey key = Registry.Users.OpenSubKey("S-1-5-20", true);
RegistrySecurity rs = new RegistrySecurity();

// Sukuriame naują naudotojo teisių įrašą ir pridedame Network Service su visais leidimais
RegistryAccessRule rule = new RegistryAccessRule("Network Service",
    RegistryRights.FullControl,
    InheritanceFlags.ContainerInherit | InheritanceFlags.ObjectInherit,
    PropagationFlags.None,
    AccessControlType.Allow);

rs.AddAccessRule(rule);

// Atnaujiname rakto permisijas su naujais leidimais
key.SetAccessControl(rs);
