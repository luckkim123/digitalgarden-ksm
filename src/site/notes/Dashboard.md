```dataview
>>LIST
>>FROM "3_Archive/32_Calendar"
>>WHERE date(substring(file.name, 0, 10)) = date(today)
>>and !contains(file.folder, "Daily Notes") and !contains(file.folder, "Done")
>>```